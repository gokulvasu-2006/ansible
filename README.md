# Ansible Infrastructure Automation

A hands-on Ansible automation project demonstrating configuration management and infrastructure automation across two RHEL servers.

## Project Overview

Automates Nginx installation, configuration, service management, and HTTP health checks using Ansible.

## Technologies Used

- Ansible
- Red Hat Enterprise Linux (RHEL)
- Nginx
- YAML
- Jinja2
- Ansible Vault
- SELinux
- Git and GitHub

## Project Structure

```text
ansible/
├── ansible-notebooks/
├── ansible-roles/
│   ├── roles/
│   │   └── nginx/
│   │       ├── defaults/
│   │       ├── handlers/
│   │       ├── tasks/
│   │       └── templates/
│   └── site.yml
├── ansible-vault/
├── notes/
├── templates/
├── inventory.example
├── ansible.cfg
└── .gitignore
```

## Features

- Automated Nginx installation on multiple RHEL servers
- Reusable Ansible roles
- Jinja2-based configuration management
- Handler-based service restarts
- SELinux port configuration
- Encrypted variables using Ansible Vault
- HTTP health checks
- Idempotent automation

## Setup

Clone the repository:

```bash
git clone https://github.com/gokulvasu-2006/ansible.git
cd ansible
```

Create your inventory:

```bash
cp inventory.example inventory
```

Edit the inventory with your server IP addresses and SSH key path.

Install the required collection:

```bash
ansible-galaxy collection install community.general
```

Check connectivity:

```bash
ansible rhel -m ping
```

## Run the Playbook

```bash
ansible-playbook ansible-roles/site.yml --syntax-check
ansible-playbook ansible-roles/site.yml
```

## Verify Nginx

```bash
ansible rhel -m uri -a "url=http://localhost:8080 return_content=yes"
```

## Security

- Do not commit private SSH keys.
- Do not commit Vault password files.
- Keep sensitive variables encrypted with Ansible Vault.
- Use a strong Vault password.

## Learning Outcomes

Developed practical experience with Ansible inventory, modules, playbooks, variables, loops, conditions, facts, templates, roles, handlers, Vault, SELinux, and idempotency.
