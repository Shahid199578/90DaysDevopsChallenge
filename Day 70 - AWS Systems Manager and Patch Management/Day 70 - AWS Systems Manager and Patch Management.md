# Day 70 - AWS Systems Manager and Patch Management

Welcome to **Day 70** of the DevOps 90-Day Challenge!
Today, we focus on **Cloud Fleet Operations**. We move away from manual server management (SSH) and learn how to use AWS Systems Manager (SSM) for automated patching, run commands, and secure access.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the architecture of the **SSM Agent**.
* Use **Session Manager** to securely connect to EC2 instances without SSH keys.
* Execute fleet-wide scripts securely using **Run Command**.
* Automate vulnerability patching across instances using **Patch Manager**.

---

## Tools Used

* **AWS Systems Manager (SSM)**
* **IAM Roles** (AmazonSSMManagedInstanceCore)
* **Amazon EC2**

---

## Key Concepts

### 1. Session Manager
Logging into servers via port 22 using PEM keys exposes your instances to security risks and is hard to scale. Session Manager natively routes terminal access directly through the browser. All sessions are fully encrypted and securely logged.

### 2. Run Command
Run Command lets you remotely and securely manage the configuration of your managed instances. You can run scripts or apply patches simultaneously across 1,000 servers with a single click, without having to SSH into any of them.

### 3. Patch Manager
Allows you to automate the process of patching managed instances with both security related and other types of updates. We define "Patch Baselines" that dictate which patches should be auto-approved and applied.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Secure Access** | Logging into `ssm-user` via IAM roles without opening any inbound ports on the Security Group. |
| **Fleet Automation** | Using Run Command to simultaneously update software packages across multiple EC2 instances. |
| **Compliance Auditing** | Logging all commands executed during a Session Manager connection to AWS CloudTrail. |

---

## Bonus (Extra Learning)

* Attempt to create an SSM Document that automatically installs an Nginx server.
* Explore AWS Systems Manager **State Manager** to ensure servers always maintain a desired configuration.

---

## Congratulations!

You have unlocked enterprise-grade server management. Managing 1 server or 10,000 servers is now the exact same amount of effort!
