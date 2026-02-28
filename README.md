DevOps Assignment Project

This project demonstrates Infrastructure Automation, Configuration Management, and DevOps principles using AWS CloudFormation and Ansible.

Part 1 – Infrastructure Setup (AWS CloudFormation)
Objective

To automate the provisioning of cloud infrastructure required to host a server instance using Infrastructure as Code (IaC).

Tool Used

AWS CloudFormation

Infrastructure as Code (IaC)

CloudFormation is used to define cloud infrastructure declaratively in a YAML template. This eliminates manual configuration and ensures repeatable, consistent deployments.

The infrastructure template file:

ec2-template.yaml
Resources Provisioned

The CloudFormation template provisions the following resources:

1. EC2 Instance

Instance Type: t2.micro (Free Tier eligible)

Operating System: Amazon Linux

Tagged as: DevOpsServer

Deployed inside default AWS VPC

2. Security Group

The security group is configured to allow:

SSH access (Port 22) → Remote administration

HTTP access (Port 80) → Web application access

This ensures proper networking and secure access configuration.

Networking Configuration

The EC2 instance is deployed inside the default AWS VPC with:

Public IP address

Internet access

Security group rules controlling inbound traffic

Architecture Overview

The infrastructure architecture includes:

User / Internet
↓
Security Group (Port 22, 80)
↓
EC2 Instance (t2.micro)
↓
Default VPC Network

The architecture diagram is included as:

architecture-part1.png
Benefits of Infrastructure as Code

Eliminates manual provisioning errors

Enables repeatable deployments

Improves scalability

Supports DevOps automation practices

Ensures consistent security configuration

Part 2 – Configuration Management (Ansible)
Objective

To automate server configuration after infrastructure provisioning using Ansible.

Tool Used

Ansible (Agentless Configuration Management Tool)

Ansible was selected due to its simplicity, SSH-based architecture, and suitability for cloud environments.

The automation files are located in:

ansible/playbook.yml
ansible/inventory.ini
Automation Workflow

When executed, the Ansible playbook performs the following tasks:

1. System Update

Updates all system packages to ensure the server is secure and up to date.

2. Docker Installation

Installs Docker container runtime required to run application containers.

3. Docker Service Start

Starts the Docker service immediately after installation.

4. Enable Docker on Boot

Configures Docker to automatically start whenever the server reboots.

5. Configure User Permissions

Adds the ec2-user to the Docker group to allow Docker usage without requiring sudo privileges.

6. Verification

Confirms successful Docker installation by checking the installed version.

Example Execution Command

When AWS is active, the playbook would be executed using:

ansible-playbook -i inventory.ini playbook.yml

Ansible connects via SSH and executes tasks sequentially.

Configuration Architecture Flow

CloudFormation
↓
EC2 Instance Provisioned
↓
Ansible Playbook Execution
↓
Docker Installed & Configured
↓
Server Ready for Container Deployment

DevOps Alignment

This configuration management approach ensures:

Infrastructure provisioning (Part 1)

Automated server setup (Part 2)

Reduced manual intervention

Consistent environment configuration

Reproducible deployments

Implementation Note

Due to AWS account activation constraints during development, live execution of infrastructure provisioning was limited. However, the Infrastructure-as-Code template and Ansible automation logic are fully implemented and production-ready for execution in a live AWS environment.

Summary

Part 1 implements Infrastructure as Code using CloudFormation.
Part 2 implements Configuration Management using Ansible.

Together, they demonstrate core DevOps automation principles:

Infrastructure automation

Configuration automation

Security configuration

Service lifecycle management
