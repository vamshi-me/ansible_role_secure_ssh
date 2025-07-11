# Ansible Role: `secure_ssh_user`

An Ansible role to automate the configuration of secure SSH access on Linux servers.  
It also hardens SSH, installs & configures Nginx with a custom web page, and supports multiple operating systems.

---

##  Features

This role performs the following tasks:

- Creates a secure non-root user.
- Adds an SSH public key for the secure user.
- Hardens SSH by disabling root login.
- Installs and configures Nginx with a custom `index.html`.
- Updates package cache (apt/yum) based on OS.
- Sets and ensures the correct web root directory exists based on OS.
- Starts & enables the Nginx service.

Supports:
- Ubuntu (18.04, 20.04, 22.04)
- Amazon Linux 2
- RedHat / EL (7, 8, 9)

---

## Pre-Requirements

- Ansible ≥ 2.6
- A running Linux host (Ubuntu, Amazon Linux, or RHEL/EL) reachable via SSH.
- A vault file (if you want to store sensitive variables securely).

---

## 🚀 Role Variables

These variables must be defined (you can use Vault to encrypt them):

| Variable            | Description                     | Example |
|---------------------|---------------------------------|---------|
| `ssh_public_key`    | SSH public key for the secure user | `ssh-rsa AAAAB3N...` |

You can store this securely in `group_vars/all/vault.yml` and encrypt it with Ansible Vault.

Example `group_vars/all/vault.yml`:
```yaml
ssh_public_key: YOUR_SSH_PUBLIC_KEY
secure_user: deployer
