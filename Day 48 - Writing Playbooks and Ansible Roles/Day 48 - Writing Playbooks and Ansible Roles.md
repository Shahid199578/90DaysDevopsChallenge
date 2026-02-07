# Day 48 - Writing Playbooks and Ansible Roles

Welcome to **Day 48** of the DevOps 90-Day Challenge!
Today, we’ll move beyond single commands and start writing **Ansible Playbooks** to orchestrate complex tasks, and learn how to structure them using **Roles**.

[![](https://img.youtube.com/vi/4FouYJkBbbQ/0.jpg)](https://www.youtube.com/watch?v=4FouYJkBbbQ)

[Watch the video](https://www.youtube.com/watch?v=4FouYJkBbbQ)

---

## Objective

By the end of this session, you will:

* Write your first **Ansible Playbook** using YAML.
* Understand the structure of **Plays**, **Tasks**, and **Modules**.
* Refactor playbooks into **Ansible Roles** for reusability.

---

## Tools Used

* **Ansible Playbooks** (YAML)
* **Visual Studio Code** (or any text editor)
* **Ansible Galaxy** (for initializing roles)

---

## Key Concepts

### 1. Ansible Playbooks

Playbooks are the language of Ansible's configuration, deployment, and orchestration. They are written in **YAML**.

**Sample `install_nginx.yml`:**

```yaml
---
- name: Install Nginx on Webservers
  hosts: webservers
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

### 2. Ansible Roles

Roles allow you to automatically load certain var_files, tasks, and handlers based on a known file structure.

**Directory Structure:**
```bash
roles/
    common/
    webservers/
        tasks/
        handlers/
        files/
        templates/
        vars/
        defaults/
        meta/
```

### 3. Creating a Role

```bash
ansible-galaxy init my_role
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Playbook** | YAML file defining the `Install Nginx` automation logic. |
| **Modules** | `apt`, `service`, `copy` modules used within tasks. |
| **Roles** | structured directory for `webserver` configuration. |
| **Variables** | defining dynamic values like `port: 80`. |

---

## Bonus (Extra Learning)

* Check out **Ansible Galaxy** to find community-contributed roles.
* Learn about **Handlers** to restart services only when configuration changes.

---

## Congratulations!

You’ve successfully written your first **Playbook** and understood how to modularize your code with **Roles**!
This is a huge step towards writing professional-grade automation.

---

## Try These Next

* Write a playbook to deploy a simple **HTML website**.
* Create a role that installs and configures **MySQL**.
