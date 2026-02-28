DevOps Assignment Project
## Part 2 – Configuration Management (Ansible)

Server configuration is automated using Ansible to ensure consistency and repeatability.

### Automation Workflow

1. Ansible connects to the EC2 instance via SSH.
2. System packages are updated.
3. Docker is installed.
4. Docker service is started.
5. Docker is configured to automatically start on boot.
6. User permissions are configured for Docker usage.

### Files Included

- ansible/playbook.yml – Ansible automation script
- ansible/inventory.ini – Target server configuration

This configuration management approach ensures that infrastructure provisioning (Part 1) is followed by automated server setup, aligning with DevOps best practices.
