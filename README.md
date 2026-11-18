# Ansible Automation Lab

A hands-on Ansible automation project demonstrating configuration management, infrastructure automation, reusable roles, Jinja2 templating, and secure secret management on RHEL-based Linux servers.

This repository documents my practical learning and implementation of Ansible through a structured, hands-on project.

## Project Overview

The goal of this project is to automate Linux server administration using Ansible.

The project includes:

- Ansible inventory and configuration management
- Ad-hoc commands and playbooks
- Variables, loops, and conditional execution
- Facts gathering and Jinja2 templates
- Handlers and idempotent automation
- Reusable Ansible roles
- Ansible Vault for sensitive data
- Nginx installation and configuration on RHEL servers
- SELinux configuration for a custom Nginx port
- HTTP health checks to verify deployment

## Technologies Used

| Technology | Purpose |
|---|---|
| Ansible | Configuration management and automation |
| Linux (RHEL) | Managed servers |
| YAML | Playbooks, variables, and task definitions |
| Jinja2 | Dynamic configuration templates |
| Nginx | Web server deployment |
| Ansible Vault | Encryption of sensitive variables |
| SSH | Secure communication with managed nodes |
| Git & GitHub | Version control and project hosting |

## Repository Structure

```text
ansible-lab/
│
├── ansible-notebooks/
│   ├── conditions.yml
│   ├── facts.yml
│   ├── firstplaybook.yml
│   ├── handlers.yml
│   ├── jinja.yml
│   ├── loops.yml
│   ├── loops1.yml
│   ├── prac.yml
│   ├── site.yml
│   └── variable.yml
│
├── ansible-roles/
│   ├── roles/
│   │   └── nginx/
│   │       ├── defaults/
│   │       ├── handlers/
│   │       ├── tasks/
│   │       ├── templates/
│   │       ├── vars/
│   │       └── README.md
│   └── site.yml
│
├── ansible-vault/
│   ├── secret.yml
│   └── vault-test.yml
│
├── templates/
│   └── serverinfo.j2
│
├── notes/
│   ├── day1
│   ├── day2
│   ├── day3
│   └── day4
│
├── ansible.cfg
├── inventory.example
└── .gitignore
```

## Environment

The lab uses:

- One Ansible control node
- Two RHEL managed nodes
- SSH connectivity between the control node and managed nodes
- Privilege escalation using `become`

## Setup Instructions

### 1. Install Ansible

Install Ansible on your Linux control node.

Verify the installation:

```bash
ansible --version
```

### 2. Clone the Repository

```bash
git clone https://github.com/gokulvasu-2006/ansible.git
cd ansible
```

### 3. Configure Inventory

Create your local inventory using the example file:

```bash
cp inventory.example inventory
```

Edit the inventory:

```bash
vim inventory
```

Replace the placeholder IP addresses and SSH private-key path with your own environment details.

Example:

```ini
[rhel]
node1 ansible_host=YOUR_NODE1_IP
node2 ansible_host=YOUR_NODE2_IP

[rhel:vars]
ansible_user=ec2-user
ansible_ssh_private_key_file=~/.ssh/YOUR_KEY.pem
```

Ensure SSH access to both managed nodes is configured.

### 4. Verify Connectivity

```bash
ansible rhel -m ping
```

## Nginx Automation Using Ansible Roles

The project includes a reusable Nginx role that automates web server configuration on RHEL managed nodes.

### Role Features

- Installs Nginx using the DNF package manager
- Starts and enables the Nginx service
- Deploys a custom Nginx configuration using a Jinja2 template
- Uses handlers to restart Nginx when its configuration changes
- Configures SELinux to allow HTTP traffic on a custom port
- Performs an HTTP health check to verify the service

### Install Required Collection

```bash
ansible-galaxy collection install community.general
```

### Run the Nginx Playbook

```bash
ansible-playbook ansible-roles/site.yml
```

The playbook configures Nginx on the managed RHEL servers using port `8080`.

### Verify Nginx

Check the service:

```bash
ansible rhel -b -m command -a "systemctl is-active nginx"
```

Test the HTTP response:

```bash
ansible rhel -m uri -a "url=http://localhost:8080 return_content=yes"
```

Expected response:

```text
Hello ansible role!
```

## Ansible Vault

Ansible Vault is used to encrypt sensitive variables and protect confidential configuration data.

View an encrypted file:

```bash
ansible-vault view ansible-vault/secret.yml
```

Edit an encrypted file:

```bash
ansible-vault edit ansible-vault/secret.yml
```

Run the Vault test playbook:

```bash
ansible-playbook ansible-vault/vault-test.yml --ask-vault-pass
```

**Security:** Never commit Vault passwords, SSH private keys, or unencrypted secrets to GitHub.

## Ansible Concepts Practiced

| Concept | Implementation |
|---|---|
| Inventory | Managing multiple RHEL hosts |
| Ad-hoc commands | Executing tasks directly on managed nodes |
| Playbooks | Automating configuration tasks |
| Variables | Reusing configurable values |
| Loops | Repeating tasks |
| Conditions | Executing tasks based on conditions |
| Facts | Gathering system information |
| Templates | Generating dynamic configuration files |
| Handlers | Restarting services when configurations change |
| Roles | Organizing reusable automation |
| Vault | Encrypting sensitive information |
| Idempotency | Ensuring repeated runs do not cause unnecessary changes |

## Learning Outcome

Through this project, I gained practical experience with Ansible automation, Linux server administration, reusable role development, secure variable management, and deploying services across multiple RHEL servers.

## Future Improvements

- Add automated syntax and lint checks
- Integrate Ansible with CI/CD pipelines
- Add more reusable roles for Linux services
- Improve monitoring and deployment verification
- Expand automation to additional Linux distributions

## Author

**Gokul Vasu**

GitHub: [@gokulvasu-2006](https://github.com/gokulvasu-2006)

Project Repository: [Ansible Automation Lab](https://github.com/gokulvasu-2006/ansible)
