# Day 68 - Tagging and Resource Management Best Practices

Welcome to **Day 68** of the DevOps 90-Day Challenge!
Today, we focus on **Tagging**. It sounds boring, but in a large environment, it's the *only* way to survive. Tags are metadata that help you organize, secure, and track costs for your resources.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand why **Tagging** is critical for Cost, Automation, and Security.
* Define a **Standard Tagging Strategy** for your organization.
* Enforce tagging using **Tag Policies** (AWS Organizations).
* Use **Resource Groups** to manage tagged resources.

---

## Tools Used

* **AWS Tag Editor** (Resource Groups)
* **AWS Cost Allocation Tags**
* **AWS Organizations** (Tag Policies)

---

## Key Concepts

### 1. Types of Tags
*   **Technical**: `Name`, `Environment` (Dev/Prod), `Version` (v1.2).
*   **Business**: `CostCenter`, `Project`, `Owner` (Team A).
*   **Security**: `Confidentiality` (Public/Private), `Compliance` (PCI/HIPAA).
*   **Automation**: `Schedule` (StartStop), `Backup` (True/False).

### 2. Cost Allocation Tags
You must explicitly **activate** user-defined tags in the Billing Console before they show up in Cost Explorer. AWS-generated tags (like `aws:createdBy`) are automatic.

### 3. Tag Editor
A tool to find untagged resources and apply tags in bulk. "Find all EC2 instances in `us-west-2` missing the `Environment` tag."

---

## Key Concepts Applied

| Concept | Application |
| :--- | :--- |
| **Standardization** | Ensuring everyone uses `Environment` and not `env`, `Env`, or `environment`. Case matters! |
| **Automation** | A script that shuts down all instances with tag `Schedule: OfficeHours` every evening. |
| **Security** | An IAM policy that allowing developers to *only* stop instances with tag `Team: Developers`. |

---

## Bonus (Extra Learning)

*   Create a **Resource Group** that contains all resources with tag `Project: Migration`.
*   Write a Config Rule to mark resources as Non-Compliant if they lack an `Owner` tag.

---

## Congratulations!

You’ve organized your cloud! Good tagging is the difference between a messy garage and a professional warehouse.

---

## Try These Next

*   Export tagging data to CSV using Tag Editor.
*   Enforce a Tag Policy that prevents creation of resources without a `CostCenter` tag.
