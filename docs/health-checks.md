# SOHO Infrastructure - Web Server Health Checks

## Overview

Ansible manages two Linux web servers.

## Infrastructure

- rocky01: Rocky Linux 9.8 running Apache
- ubuntu01: Ubuntu 26.04 running NGINX

## Health Checks

Ansible uses the URI module to verify HTTP responses.

Expected result: HTTP 200 OK.

### Rocky Linux Apache

Command: ansible rocky -m ansible.builtin.uri -a "url=http://127.0.0.1 status_code=200"

Result: HTTP 200 PASS

### Ubuntu NGINX

Command: ansible ubuntu -m ansible.builtin.uri -a "url=http://127.0.0.1 status_code=200"

Result: HTTP 200 PASS

## Deployment

Command: ansible-playbook playbooks/site.yml -K

Deployment result:
- Rocky Linux: successful
- Ubuntu: successful
- Failed tasks: 0
- Changed tasks on final run: 0

## Skills Demonstrated

- Ansible automation
- Linux system administration
- Apache and NGINX administration
- YAML configuration
- HTTP health checks
- Idempotent infrastructure automation
- Technical documentation
