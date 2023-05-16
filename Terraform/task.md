# Terraform

## Requirements:

- Create a _Terraform_ module for provisioning one _AWS_/_Azure_/_GCP_/_OCI_/... (cloud provider of your choice) compute instance (VM);
- Provision one SSH public key for the created instance;
- Provision and attach static IP to the instance;
- Install and configure docker on the instance;
- Run _Grafana_ container in _Docker_ so that it is accessible from the web, i.e. `http://<IP-ADDRESS>:<PORT>/dashboards`;
- Provide instructions along with the code on _GitHub_ (or other VCS platform of your choice).

### Additional:

- Make use of varibales;
- Make use of outputs.

## Optional:

- Make use of _Ansible_ playbooks for configuration management;
- Add custom _Grafana_ dashboards to observe specific metrics.

##Implementation: </br>
Below is a Terraform module that provisions an AWS EC2 instance, attaches a static IP, installs and configures Docker, and runs a Grafana container accessible via a web browser.

To get started, lets create a new directory for new Terraform project and initialize it:

```bash
mkdir terraform-aws-grafana
cd terraform-aws-grafana
```

1) Сreating a Terraform module directory structure:

```
terraform-aws-grafana/
  ├── main.tf
  ├── variables.tf
  ├── outputs.tf
  └── ansible/
        └── grafana.yml
```

2) Сreating the module files.

`main.tf`:

```hcl
# Configure AWS provider
provider "aws" {
  region = var.aws_region
}

resource "aws_key_pair" "ssh_key" {
  key_name   = var.ssh_key_name
  public_key = var.ssh_public_key
}

resource "aws_instance" "grafana_instance" {
  ami           = var.instance_ami
  instance_type = var.instance_type
  key_name      = aws_key_pair.ssh_key.key_name

  tags = {
    Name = "grafana-instance"
  }
}

resource "aws_eip" "grafana_ip" {
  instance = aws_instance.grafana_instance.id
}

resource "null_resource" "configure_instance" {
  depends_on = [aws_eip.grafana_ip]

  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common",
      "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -",
      "sudo add-apt-repository \"deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable\"",
      "sudo apt-get update",
      "sudo apt-get install -y docker-ce",
      "sudo usermod -aG docker ubuntu"
    ]
  }

  provisioner "remote-exec" {
    inline = [
      "sudo docker run -d -p 3000:3000 --name=grafana grafana/grafana"
    ]
  }

  connection {
    type        = "ssh"
    host        = aws_eip.grafana_ip.public_ip
    user        = "USERNAME"
    private_key = file(var.ssh_private_key_path)
  }
}

output "grafana_ip_address" {
  value = aws_eip.grafana_ip.public_ip
}

# Create a security group allowing SSH and HTTP traffic
resource "aws_security_group" "instance_sg" {
  name        = "instance_sg"
  description = "Security group for the instance"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Provision EC2 instance
resource "aws_instance" "example_instance" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name
  security_group_ids = [aws_security_group.instance_sg.id]
  user_data     = filebase64("${path.module}/scripts/userdata.sh")

  tags = {
    Name = "example-instance"
  }
}


# Create an elastic IP
resource "aws_eip" "example_eip" {
  instance = aws_instance.example_instance.id

  vpc = true

  tags = {
    Name = "example-eip"
  }
}

# Output instance and EIP information
output "instance_id" {
  value = aws_instance.example_instance.id
}

output "public_ip" {
  value = aws_eip.grafana_ip.public_ip
}


```

`variables.tf`:
```hcl
variable "aws_access_key" {
  description = "AWS access key"
}

variable "aws_secret_access_key" {
  description = "AWS secret access key"
}

variable "aws_region" {
  description = "AWS region"
  default     = "us-west-2"
}

variable "ami" {
  description = "AMI ID"
  default     = "ami-12345678"
}

variable "instance_type" {
  description = "EC2 instance type"
  default     = "t2.micro"
}

variable "key_name" {
  description = "SSH key pair name"
}

variable "instance_name" {
  description = "Name of the EC2 instance"
  default     = "grafana-instance"
}

variable "elastic_ip_name" {
  description = "Name of the Elastic IP"
  default     = "grafana-elastic-ip"
}

```

`outputs.tf`:
```hcl
output "instance_id" {
  description = "ID of the created EC2 instance"
  value       = aws_instance.grafana_instance.id
}

output "public_ip" {
  description = "Public IP of the created EC2 instance"
  value       = aws_instance.grafana_instance.public_ip
}

}
```

3) To adding Ansible playbooks for configuration management, need create a separate directory named `ansible` and place playbooks inside it. </br>
Lets create an Ansible playbook named `grafana.yml` with the following contents:

```yaml
# ansible/grafana.yml

- name: Install Docker
  hosts: all
  become: true

  tasks:
    - name: Install Docker dependencies
      apt:
        name:
          - apt-transport-https
          - ca-certificates
          - curl
          - gnupg
          - lsb-release
        state: present

    - name: Add Docker GPG key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker APT repository
      apt_repository:
        repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_lsb.codename }} stable
        state: present

    - name: Update APT cache
      apt:
        update_cache: yes

    - name: Install Docker
      apt:
        name: docker-ce
        state: present

    - name: Start Docker service
      service:
        name: docker
        state: started

- name: Run Grafana container
  hosts: all
  become: true

  tasks:
    - name: Pull Grafana Docker image
      docker_image:
        name: grafana/grafana:latest
        source: pull

    - name: Create Grafana container
      docker_container:
        name: grafana
        image: grafana/grafana:latest
        state: started
        restart_policy: always
        ports:
          - "3000:3000"
          
```

With the above structure, we can create a GitHub repository and push the Terraform module, variables, and Ansible playbooks. 

To use the module, need create a separate Terraform configuration file (`main.tf`) where specify the module and configure any necessary inputs:

```hcl
# main.tf

module "aws_instance" {
  source = "github.com/<username>/<repository>"

  aws_region      = "us-east-1"
  ami_id          = "ami-12345678"
  instance_type   = "t2.micro"
  key_name        = "example-key"
  ssh_public_key  = "ssh-rsa ABCDEFG..."
}
```

After configuring the module, ninitialize and apply the Terraform configuration:

```bash
terraform init
terraform apply
```
Important: before running Terraform commands, you must set up the required AWS credentials with the appropriate rights.

4) Adding custom _Grafana_ dashboards to observe specific metrics to observe specific metrics in a Terraform module:

```hcl
resource "grafana_dashboard" "CPU" {
  dashboard_json = <<EOF
{
  "editable": true,
  "panels": [
    {
      "id": 1,
      "title": "Custom Metric",
      "type": "graph",
      "datasource": "${grafana_datasource.example.id}",
      "targets": [
        {
          "refId": "A",
          "expr": "my_custom_metric{instance=\"${var.instance_id}\", region=\"${var.region}\"}"
        }
      ],
      "gridPos": {
        "x": 0,
        "y": 0,
        "w": 12,
        "h": 8
      }
    }
  ]
}
EOF
}

resource "grafana_datasource" "CPU" {
  name            = "Prometheus"
  type            = "prometheus"
  url             = "http://prometheus.example.com"
  access_mode     = "proxy"
  basic_auth      = "true"
  basic_auth_user = "admin"
  basic_auth_password = "password"
}

```

We're use the `grafana_dashboard` resource to create a custom Grafana dashboard. The `dashboard_json` argument contains the JSON representation of the dashboard configuration.</br>
In this case, we have a single panel of type "graph" that visualizes a custom metric.

The `grafana_datasource` resource is used to configure the Prometheus data source for the dashboard.

Important: Need have the necessary provider and data source blocks defined in your Terraform configuration to connect to Grafana and Prometheus.



