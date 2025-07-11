# Ansible Role: Secure SSH User & Nginx Setup

This Ansible role automates the configuration of a secure SSH user, hardens SSH, and sets up Nginx with a custom web page.

It demonstrates:

* Configuring secure SSH access & hardening
* Installing and configuring Nginx with a custom web page
* Managing sensitive credentials with Ansible Vault
* Supporting multiple operating systems (Ubuntu, Amazon Linux & RedHat)

---

## 📂 Role Structure

```
ansible_role_secure_ssh/
├── defaults/
│   └── main.yml              # Default variables
├── handlers/
│   └── main.yml              # Handlers (e.g., restart ssh)
├── meta/
│   └── main.yml              # Role metadata
├── tasks/
│   └── main.yml              # Main tasks
├── templates/
│   └── index.html.j2         # Custom Nginx index page
├── tests/
│   ├── inventory             # Sample inventory
│   └── test.yml              # Test playbook
├── vars/
│   └── main.yml              # Additional variables (if any)
├── LICENSE                   # MIT License
├── .gitignore                # Git ignore file
└── README.md                 # This file
```

---

## 🚀 Role Variables

These variables can be defined:

| Variable         | Description                                                                   | Example              |
| ---------------- | ----------------------------------------------------------------------------- | -------------------- |
| `username`       | Username for the secure user (defaults to `ansible_user`)                     | `deployer`           |
| `ssh_public_key` | SSH public key for the secure user (sensitive, recommended to store in vault) | `ssh-rsa AAAAB3N...` |

You can override `username` if needed.
You **must provide `ssh_public_key`**, and it is recommended to keep it encrypted with Ansible Vault.

---

## 🔐 Pre-requisite: Create the Vault file

This project uses Ansible Vault to securely store the sensitive `ssh_public_key`.

1️⃣ Create the vault file:

```bash
ansible-vault create group_vars/all/vault.yml
```

2️⃣ Add the following content:

```yaml
ssh_public_key: YOUR_SSH_PUBLIC_KEY
```

3️⃣ To edit later:

```bash
ansible-vault edit group_vars/all/vault.yml
```

4️⃣ Run playbook with vault password file:

```bash
ansible-playbook -i inventory configure.yml --vault-password-file vault.pass
```

---

## 🔧 Tasks Performed by the Role

✅ Create a secure user
✅ Add SSH key for the user
✅ Harden SSH: disable root login
✅ Install Nginx
✅ Update package cache (apt/yum) depending on OS
✅ Set web root path depending on OS
✅ Ensure web root directory exists
✅ Deploy custom `index.html`
✅ Ensure Nginx is started and enabled

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 📄 .gitignore

This repo includes a `.gitignore` that ignores:

```
*.retry
*.log
*.swp
*.pyc
__pycache__/
.vscode/
.idea/
vault.pass
group_vars/all/vault.yml
```

---

## 📑 Example Playbook

```yaml
- name: Configure Secure SSH & Nginx
  hosts: all
  become: yes
  vars_files:
    - group_vars/all/vault.yml
  roles:
    - role: ansible_role_secure_ssh
```

---

## 🌐 Supported Platforms

* Ubuntu: 18.04, 20.04, 22.04
* Amazon Linux: 2
* RedHat / EL: 7, 8, 9

---

## 🤝 Contributing

Contributions and improvements are welcome. Please open an issue or PR!

---

## 📬 Author

**Vamshi Megavath**

[GitHub Profile](https://github.com/vamshi-me)

---
