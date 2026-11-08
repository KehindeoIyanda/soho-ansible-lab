# Windows File Server Configuration

## Overview

This project uses Ansible to configure a Windows 10 Home
computer as a network file server.

The Windows computer is managed remotely from RockyServer.

## Infrastructure

| Component | Configuration |
|---|---|
| Control Node | Rocky Linux 9.8 |
| Managed Windows Host | Windows 10 Home |
| Management Protocol | WinRM over HTTPS |
| WinRM Port | 5986 |
| File Sharing Protocol | SMB |
| SMB Port | 445 |
| Share Name | SOHO-Shared |
| Shared Folder | C:\SOHO\Shared |

## Ansible Implementation

Role:

`roles/windows_fileserver/tasks/main.yml`

The role performs these tasks:

1. Creates the shared directory.
2. Creates the SOHO-Shared network share.
3. Grants the Administrators group full share access.

## Security Configuration

- WinRM uses HTTPS.
- NTLM authentication is configured.
- Windows credentials are stored using Ansible Vault.
- Windows certificate trust is configured on RockyServer.
- SMB access uses Windows account authentication.

## Validation and Testing

The following tests were successful:

- Ansible WinRM connectivity test (`win_ping`).
- Shared directory creation.
- SMB share creation.
- TCP port 445 connectivity.
- SMB authentication from RockyServer.
- SMB directory listing.
- File upload from RockyServer to Windows.
- File content verification on Windows.

## SMB File Transfer Test

A test file was created on RockyServer:

`/tmp/rocky-smb-test.txt`

It was uploaded to:

`C:\SOHO\Shared\rocky-smb-test.txt`

Verified file contents:

`Created by RockyServer using SMB`

## Result

The Windows file-sharing configuration is operational.

RockyServer can authenticate to the Windows SMB share,
read its contents, and upload files successfully.
