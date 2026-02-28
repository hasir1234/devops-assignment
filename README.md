Part 1 – Infrastructure Setup Using Infrastructure as Code

The infrastructure layer of this project is implemented using AWS CloudFormation, which enables automated provisioning of cloud resources through declarative configuration templates. Instead of manually creating resources through the AWS console, infrastructure components are defined in a YAML template (ec2-template.yaml) to ensure repeatability, consistency, and version control.

The CloudFormation template defines an EC2 instance deployed within the default AWS Virtual Private Cloud (VPC). The selected instance type is t2.micro, which aligns with AWS Free Tier eligibility while remaining sufficient for lightweight application hosting. This instance represents the compute layer responsible for running the containerized application in subsequent stages of the project.

A dedicated security group is configured as part of the template to manage inbound traffic. The security configuration permits:

SSH access (Port 22) for administrative connectivity.

HTTP access (Port 80) for web application exposure.

By explicitly defining these rules, the infrastructure ensures controlled external access while maintaining security boundaries. The template approach eliminates configuration drift and ensures that identical infrastructure can be provisioned across multiple environments.

The architectural representation of this deployment is illustrated in architecture-part1.png, which outlines the relationship between the internet gateway, security group, EC2 instance, and the underlying network environment.

This implementation demonstrates the core principle of Infrastructure as Code (IaC), where infrastructure becomes programmable, version-controlled, and reproducible. Such an approach improves deployment reliability, enhances collaboration, and aligns with modern DevOps practices.

Part 2 – Configuration Management Using Ansible

Following infrastructure provisioning, configuration management is implemented using Ansible to automate the setup of the EC2 instance. Configuration management ensures that the provisioned infrastructure is prepared consistently for application deployment without manual intervention.

Ansible was selected due to its agentless architecture, SSH-based communication model, and strong support for declarative automation. The configuration logic is defined within ansible/playbook.yml, while target host definitions are specified in ansible/inventory.ini.

The playbook automates several essential server configuration tasks. These include updating system packages, installing Docker as the container runtime environment, starting the Docker service, enabling it to launch automatically on system boot, and configuring user permissions to allow container execution without elevated privileges.

By codifying server configuration, this approach eliminates inconsistencies that often arise from manual setup processes. Ansible ensures idempotent execution, meaning repeated runs of the playbook will maintain the desired system state without introducing unintended changes.

The integration of CloudFormation (infrastructure provisioning) and Ansible (configuration management) reflects a layered DevOps architecture in which infrastructure and configuration concerns are separated but automated cohesively. This structured automation enhances scalability, operational efficiency, and reliability.

Together, Part 1 and Part 2 establish the foundational environment required for container deployment in subsequent phases of the project, while demonstrating core DevOps principles of automation, consistency, and maintainability.
