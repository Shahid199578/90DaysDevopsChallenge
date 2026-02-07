# Day 50 - Ansible Best Practices and Secrets Management

Welcome to **Day 50** of the DevOps 90-Day Challenge!
Today, we’ll level up our Ansible skills by learning **Best Practices** and how to secure sensitive data using **Ansible Vault**.

[![](https://img.youtube.com/vi/qlakf5UhGck/0.jpg)](https://www.youtube.com/watch?v=qlakf5UhGck)

[Watch the video](https://www.youtube.com/watch?v=qlakf5UhGck)

---

## Objective

By the end of this session, you will:

* Structure your Ansible projects effectively.
* Encrypt sensitive data (passwords, keys) using **Ansible Vault**.
* Manage variables using `group_vars` and `host_vars`.

---

## Tools Used

* **Ansible Vault**
* **Git** (for versioning encrypted files)
* **Standard Project Layout**

---

## Key Concepts

### 1. Ansible Best Practices

* **Use Roles**: Don't write everything in one huge playbook.
* **Readable Names**: Name every task clearly.
* **Version Control**: Everything goes into Git.
* **Separation**: Keep inventory separate from playbooks.

### 2. Ansible Vault

Vault allows you to encrypt YAML files.

```bash
# Create a new encrypted file
ansible-vault create secrets.yml

# Edit an encrypted file
ansible-vault edit secrets.yml

# Encrypt an existing file
ansible-vault encrypt existing_file.yml
```

### 3. Running with Vault

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Security** | Encrypting DB passwords in `group_vars/all/passwords.yml`. |
| **Modularity** | Using `site.yml` to import other playbooks. |
| **Variable Precedence** | Understanding how `group_vars` override defaults. |

---

## Bonus (Extra Learning)

* Set up a **Vault Password File** so you don't have to type it every time (add it to `.gitignore`!).
* Use **multiple vault passwords** for different environments (dev/prod).

---

## Congratulations!

You’ve successfully secured your automation using **Ansible Vault** and cleaned up your project structure!
Security is a critical part of DevOps, and you're doing it right.

---

## Try These Next

* Refactor your previous project to follow the **Standard Directory Layout**.
* storing your vault password in a secured Jenkins credential used during pipeline runs.
