# Together, the access key ID and secret access key allow users to interact with AWS resources via SDKs, CLI tools, or APIs

# AWS access_key and secret_key store in aws cli configure due to security reason.
# By default it will stored in "%USERPROFILE%\.aws\config" and "%USERPROFILE%\.aws\credentials" on Windows OS
provider "aws" {
  region      = "us-west-1"
  # access_key  = ""
  # secret_key  = ""
}

# RSA key of size 4096 bits
resource "tls_private_key" "rsa_4096" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "demo_pair" {
  key_name   = "bca_project_DevOps"
  public_key = tls_private_key.rsa_4096.public_key_openssh
}

resource "local_file" "private_key" {
  content  = tls_private_key.rsa_4096.private_key_pem
  filename = "bca_project_DevOps"
}

# Creating security group and attached with our instance
resource "aws_security_group" "bca_sg" {
  name        = "bca_project_DevOps_sg"
  description = "Managed from terraform"
}

resource "aws_vpc_security_group_ingress_rule" "allow_tls_ipv4" {
  security_group_id = aws_security_group.bca_sg.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 8080
  ip_protocol       = "tcp"
  to_port           = 8080
}

resource "aws_vpc_security_group_ingress_rule" "allow_ssh" {
  security_group_id = aws_security_group.bca_sg.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 22
  ip_protocol       = "tcp"
  to_port           = 22
}

resource "aws_vpc_security_group_egress_rule" "allow_all_traffic_ipv4" {
  security_group_id = aws_security_group.bca_sg.id
  cidr_ipv4         = "0.0.0.0/0"
  ip_protocol       = "-1" # semantically equivalent to all ports
}

# In Terraform, the aws_instance resource is used to create, configure, and manage an Amazon EC2 (Elastic Compute Cloud) instance directly through IaC definitions.
# A resource block as below declares a resource of a given type "aws_instance" with a given local name "bca_ec2".
resource "aws_instance" "bca_ec2" {
  ami                    = "ami-0e6be795b21969e1d"
  instance_type          = "t2.micro"
  key_name               = aws_key_pair.demo_pair.key_name
  vpc_security_group_ids = [aws_security_group.bca_sg.id]

  user_data = <<-EOF
    #!/bin/bash
    yum update -y
    sudo dnf install java-17-amazon-corretto -y
    sudo dnf install java-11-amazon-corretto -y
    java -version
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
    sudo dnf install jenkins -y
    sudo systemctl enable jenkins
    sudo systemctl start jenkins
  EOF

  provisioner "remote-exec" {
    inline = [
      "while ! sudo test -f /var/lib/jenkins/secrets/initialAdminPassword; do echo 'Waiting for Jenkins setup...'; sleep 50; done",
      "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"
    ]

    connection {
      type        = "ssh"
      user        = "ec2-user"
      private_key = tls_private_key.rsa_4096.private_key_pem
      host        = self.public_ip
    }
  }

  tags = {
    Name = "ec2_project"
  }
}

output "bca_ec2" {
  value = aws_instance.bca_ec2.public_ip
}
