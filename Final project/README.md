Started by GitHub push by korotetskiy
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/Build-autoTriger-from-GitHub
The recommended git tool is: NONE
using credential ba8263f2-4fd8-45ab-a164-64d0a59e4d5e
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Build-autoTriger-from-GitHub/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/korotetskiy/Case.git # timeout=10
Fetching upstream changes from https://github.com/korotetskiy/Case.git
 > git --version # timeout=10
 > git --version # 'git version 2.25.1'
using GIT_ASKPASS to set credentials 
 > git fetch --tags --force --progress -- https://github.com/korotetskiy/Case.git +refs/heads/*:refs/remotes/origin/* # timeout=10
Seen branch in repository origin/main
Seen 1 remote branch
 > git show-ref --tags -d # timeout=10
Checking out Revision 344a392df62473be24f94b67c2ca59444681956a (origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 344a392df62473be24f94b67c2ca59444681956a # timeout=10
Commit message: "Update index.html"
 > git rev-list --no-walk 94482ed3af6f3b64fe348c5142f702aeb7593c4e # timeout=10
[Build-autoTriger-from-GitHub] $ /bin/sh -xe /tmp/jenkins13590376179927619756.sh
+ bash /home/vkor/myscripts/terraform_run.sh
Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.my_webserver will be created
  + resource aws_instance my_webserver {
      + ami                                  = ami-0c9978668f8d55984
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = t3.micro
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + Name  = Web Server Build by Terraform
          + Owner = Vladimir Korotetskiy
        }
      + tags_all                             = {
          + Name  = Web Server Build by Terraform
          + Owner = Vladimir Korotetskiy
        }
      + tenancy                              = (known after apply)
      + user_data                            = 4604abd4091c8460d10be1c32dd847cb90f47233
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)

      + capacity_reservation_specification {
          + capacity_reservation_preference = (known after apply)

          + capacity_reservation_target {
              + capacity_reservation_id                 = (known after apply)
              + capacity_reservation_resource_group_arn = (known after apply)
            }
        }

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + tags                  = (known after apply)
          + throughput            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + enclave_options {
          + enabled = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + maintenance_options {
          + auto_recovery = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
          + instance_metadata_tags      = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_card_index    = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + private_dns_name_options {
          + enable_resource_name_dns_a_record    = (known after apply)
          + enable_resource_name_dns_aaaa_record = (known after apply)
          + hostname_type                        = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + tags                  = (known after apply)
          + throughput            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

  # aws_security_group.my_webserver will be created
  + resource aws_security_group my_webserver {
      + arn                    = (known after apply)
      + description            = My First SecurityGroup
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + 0.0.0.0/0,
                ]
              + description      = 
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = -1
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + 0.0.0.0/0,
                ]
              + description      = 
              + from_port        = 443
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = tcp
              + security_groups  = []
              + self             = false
              + to_port          = 443
            },
          + {
              + cidr_blocks      = [
                  + 0.0.0.0/0,
                ]
              + description      = 
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = tcp
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
        ]
      + name                   = WebServer Security Group1
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = {
          + Name  = Web Test SecurityGroup
          + Owner = Vladimir Korotetskiy
        }
      + tags_all               = {
          + Name  = Web Test SecurityGroup
          + Owner = Vladimir Korotetskiy
        }
      + vpc_id                 = vpc-0010e72f4ded5b743
    }

Plan: 1 to add, 0 to change, 0 to destroy.

aws_security_group.my_webserver: Creating...
aws_security_group.my_webserver: Creation complete after 4s [id=sg-0f788caffce77276f]
aws_instance.my_webserver: Creating...
aws_instance.my_webserver: Still creating... [10s elapsed]
aws_instance.my_webserver: Creation complete after 14s [id=i-077c6e7d8b7205fe2]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
[Build-autoTriger-from-GitHub] $ /bin/sh -xe /tmp/jenkins12929228947790695538.sh
+ bash /home/vkor/myscripts/copy_from_git_to_testserver.sh
Data from the GitHub repository is copied to the test server ID:i-077c6e7d8b7205fe2 (Web Server Build by Terraform)
[Build-autoTriger-from-GitHub] $ /bin/sh -xe /tmp/jenkins10953640644707488961.sh
+ bash /home/vkor/myscripts/test1.sh
The code integrity test is PASSED
[Build-autoTriger-from-GitHub] $ /bin/sh -xe /tmp/jenkins12719225113701145548.sh
+ bash /home/vkor/myscripts/test2.sh
Load test server ID:i-077c6e7d8b7205fe2 (Web Server Build by Terraform) - PASSED
SSH: Connecting from host [jsrv]
SSH: Connecting with configuration [Web-Production] ...
SSH: EXEC: completed after 202 ms
SSH: Disconnecting configuration [Web-Production] ...
SSH: Transferred 10 file(s)
Build step 'Send files or execute commands over SSH' changed build result to SUCCESS
Finished: SUCCESS``
