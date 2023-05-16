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

Implementation: 
Below is a Terraform module that provisions an AWS EC2 instance, attaches a static IP, installs and configures Docker, and runs a Grafana container accessible via a web browser.

1) Сreating a Terraform module directory structure:

```
terraform-module/
  ├── main.tf
  ├── variables.tf
  ├── outputs.tf
  └── scripts/
        └── userdata.sh
```

2) Сreating the module files.

`main.tf`:

```hcl
# Configure AWS provider
provider "aws" {
  region = var.aws_region
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
  value = aws_eip.example_eip.public_ip
}

```

`variables.tf`:
```hcl
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "ami_id" {
  description = "AMI ID"
  type        = string
  default     = "ami-0c94855ba95c71c99" # Ubuntu 20.04 LTS
}

variable "instance_type" {
  description = "Instance type"
  type        = string
  default     = "t2.micro"
}

variable "key_name" {
  description = "SSH key pair name"
  type        = string
  default     = "example-keypair"
}
```

`outputs.tf`:
```hcl
output "grafana_url" {
  value = "http://${aws_eip.example_eip.public_ip}:3000/dashboards"
}
```

`userdata.sh` (located in the `scripts/` directory):
```bash
#!/bin/bash

# Install Docker
apt-get update
apt-get install -y docker.io

# Add current user to the docker group
usermod -aG docker $USER

# Start Grafana container
docker run -d -p 3000:3000 --name grafana grafana/grafana
```

This module sets up an AWS EC2 instance, attaches a static IP to it,
