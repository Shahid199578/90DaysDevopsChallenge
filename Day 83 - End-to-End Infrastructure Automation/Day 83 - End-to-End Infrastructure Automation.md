# Day 83 - End-to-End Infrastructure Automation

Welcome to **Day 83** of the DevOps 90-Day Challenge!
We have built pieces. Now we build the whole car. Today is about **Orchestration**. How do Terraform, Ansible, and Packer work together?

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Build a **Golden AMI** using **Packer**.
* Provision infrastructure using **Terraform** (using the Golden AMI).
* Configure the instance using **Ansible** (post-provisioning).
* Glue it all together in a **GitHub Actions** workflow.

---

## Tools Used

* **Packer** (Image Builder)
* **Terraform** (Infrastructure Provisioner)
* **Ansible** (Config Manager)
* **GitHub Actions**

---

## Key Concepts

### 1. Immutable Infrastructure
Instead of patching servers (Mutable), we bake a new Image (Amazon Machine Image) with the latest patches and code, deploy it, and delete the old servers.
**Packer** automates this baking.

### 2. The Chain
1.  **Packer**: Builds `ami-123` containing Nginx + PHP + Security patches.
2.  **Terraform**: Reads `ami-123` ID and launches an Auto Scaling Group.
3.  **Ansible**: (Optional) Connects to the new instances to register them with Monitoring/Logging agents (dynamic config).

### 3. Idempotency
Running the pipeline twice shouldn't break anything. Terraform checks state. Packer creates a new AMI only if code changed.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **User Data** | passing a script to Terraform to bootstrap the instance on launch. |
| **Dynamic Inventory** | Ansible querying AWS API to find "all instances with tag Role:Web" instead of a static IP list. |
| **Secrets** | Passing AWS Credentials securely through all 3 tools. |

---

## Bonus (Extra Learning)

*   Use **Terraform Null Resource** to trigger Ansible playbooks from within Terraform (Tricky/Advanced).
*   Implement **Green/Blue AMI updates** (Replace ASG instances slowly).

---

## Congratulations!

You have automated the entire server lifecycle. From empty account to running application with zero clicks.

---

## Try These Next

*   Build a Docker image with Packer (instead of AMI).
*   Add **InSpec** to verify the AMI was built correctly.
