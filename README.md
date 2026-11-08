# SOHO Ansible Home Lab

A multi-platform infrastructure automation project using Ansible to configure and manage Rocky Linux, Ubuntu Linux, and Windows 10 Home systems from a centralized Rocky Linux control node.

## Project Overview

This project demonstrates practical IT infrastructure administration and configuration management in a Small Office/Home Office (SOHO) environment.

Ansible automates Linux web server configuration, Windows file sharing, system administration, and connectivity validation across multiple operating systems.

## Infrastructure Architecture

| Component | Operating System | Function |
|---|---|---|
| Control Node | Rocky Linux 9.8 | Ansible automation |
| Managed Node 1 | Rocky Linux 9.8 | Apache web server |
| Managed Node 2 | Ubuntu Linux 26.04 | NGINX web server |
| Managed Node 3 | Windows 10 Home | SMB network file server |

### Architecture Diagram

```text
                 Ansible Control Node
                    Rocky Linux 9.8
                          |
             +------------+------------+
             |            |            |
          SSH/Local      SSH       WinRM HTTPS
             |            |            |
        Rocky Linux     Ubuntu      Windows 10
          Apache        NGINX       SMB Server
                                      |
                                 SOHO-Shared
                                  Network Share
```

## Technologies Used

- Ansible Core 2.15
- Rocky Linux 9.8
- Ubuntu Linux 26.04
- Windows 10 Home
- Python 3
- OpenSSH
- WinRM over HTTPS
- NTLM authentication
- SMB file sharing
- Apache HTTP Server
- NGINX
- Ansible Vault
- Git and GitHub

## Project Structure

```text
soho-ansible-lab/
├── ansible.cfg
├── .gitignore
├── inventory/
│   ├── hosts.ini
│   └── group_vars/
│       └── windows/
│           └── main.yml
├── playbooks/
│   ├── site.yml
│   ├── system_audit.yml
│   └── windows.yml
├── roles/
│   ├── rocky_web/
│   ├── ubuntu_app/
│   └── windows_fileserver/
└── docs/
    ├── health-checks.md
    └── windows-fileserver.md
```

## Automation Implemented

### Linux Server Configuration

- Automated Apache installation and service management on Rocky Linux.
- Automated NGINX installation and service management on Ubuntu.
- Managed services through reusable Ansible roles.
- Configured and validated Linux web server availability.

### Windows File Server Configuration

- Configured Windows 10 Home for SMB network file sharing.
- Created the `C:\SOHO\Shared` directory.
- Created the `SOHO-Shared` network share.
- Configured share permissions for Administrators.
- Managed Windows remotely using WinRM over HTTPS.

### Security Implementation

- Encrypted Windows credentials using Ansible Vault.
- Configured certificate trust for WinRM HTTPS.
- Used SSH for Linux remote administration.
- Excluded certificates, trust bundles, and encrypted credential files from Git.

## Validation and Testing

The following operations have been successfully tested:

- Ansible connectivity to Linux managed nodes.
- Windows WinRM connectivity using `win_ping`.
- Apache and NGINX service deployment.
- Windows shared directory creation.
- SMB share creation and authentication.
- SMB directory listing from Rocky Linux.
- File upload from Rocky Linux to Windows.
- Verification of uploaded file contents on Windows.

## Getting Started

### Prerequisites

- A Rocky Linux control node.
- Rocky Linux, Ubuntu, and Windows managed systems.
- Ansible Core installed on the control node.
- SSH access to Linux nodes.
- WinRM HTTPS configured on Windows.
- Python and required Ansible collections.

### Clone the Repository

```bash
git clone https://github.com/KehindeoIyanda/soho-ansible-lab.git
cd soho-ansible-lab
```

### Configure the Inventory

Edit:

`inventory/hosts.ini`

Replace the sample Ubuntu address with your managed Ubuntu machine's IP address. Configure the Windows hostname or IP address for your environment.

### Configure Windows Credentials

Create your encrypted Vault file at:

`inventory/group_vars/windows/vault.yml`

Store the Windows password as the `vault_windows_password` variable using Ansible Vault.

Do not commit passwords, certificates, or private keys.

### Run Linux Automation

```bash
ansible-playbook playbooks/site.yml -K
```

### Run Windows Automation

```bash
ansible-playbook playbooks/windows.yml --ask-vault-pass
```

## Documentation

- [Linux Health Checks](docs/health-checks.md)
- [Windows File Server Configuration](docs/windows-fileserver.md)

## Project Goals

This project demonstrates hands-on experience with:

- Linux system administration.
- Windows infrastructure administration.
- Configuration management.
- Infrastructure automation.
- Network services and file sharing.
- Remote administration and security.
- Technical documentation and troubleshooting.

## Author

**Kehinde O. Iyanda**

GitHub: [KehindeoIyanda](https://github.com/KehindeoIyanda)
