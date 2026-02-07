# Day 47 - Introduction to Ansible and Configuration Management

Welcome to **Day 47** of the DevOps 90-Day Challenge!
Today, we’ll dive into **Configuration Management** with **Ansible**, exploring how to automate server setup and management.

[![](https://img.youtube.com/vi/oIHRghjLfTM/0.jpg)](https://www.youtube.com/watch?v=oIHRghjLfTM)

[Watch the video](https://www.youtube.com/watch?v=oIHRghjLfTM)

---

## Objective

By the end of this session, you will:

* Understand the concepts of **Configuration Management**.
* Install and configure **Ansible** on a control node.
* Setup **Passwordless SSH** between control and managed nodes.
* Run your first **Ad-Hoc** Ansible commands.

---

## Tools Used

* **Ansible** (Control Node)
* **Linux Servers** (Managed Nodes - e.g., Ubuntu/CentOS)
* **SSH** (Secure Shell)
* **Python** (Required on managed nodes)

---

## Key Concepts

### 1. What is Ansible?

Ansible is an open-source automation tool used for **configuration management**, **application deployment**, and **task automation**. It is **agentless**, meaning it doesn't require any software to be installed on the managed nodes, just SSH.

### 2. Architecture

* **Control Node**: The machine where Ansible is installed and from where commands are run.
* **Managed Nodes**: The servers being configured.
* **Inventory**: A text file that lists the IP addresses or hostnames of managed nodes.

### 3. Inventory File Example

```ini
[webservers]
192.168.1.10
192.168.1.11

[dbservers]
192.168.1.20
```

### 4. Ad-Hoc Commands

Run a command across all servers without writing a playbook:

```bash
# Ping all servers
ansible all -m ping -i inventory.txt

# Check uptime
ansible all -a "uptime" -i inventory.txt
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Agentless** | No software installed on `webservers`, only SSH access used. |
| **Inventory** | `hosts` file defining the group of servers to manage. |
| **Ad-Hoc Commands** | `ansible -m ping` to test connectivity quickly. |
| **Idempotency** | Ensuring a task (like installing a package) changes state only if needed. |

---

## Bonus (Extra Learning)

* Explore **Ansible Configuration file (`ansible.cfg`)** settings.
* Learn about **Dynamic Inventory** for cloud environments (AWS/Azure).

---

## Congratulations!

You’ve successfully set up your **Ansible environment** and established connectivity with your managed nodes!
This is the foundation for creating complex automation playbooks.

---

## Try These Next

* Try installing **Apache/Nginx** using an ad-hoc command.
* Create a custom group in your inventory file for **database servers**.
