# Day 65 - Compliance Tools: AWS Config, Security Hub, Trusted Advisor

Welcome to **Day 65** of the DevOps 90-Day Challenge!
Today, we focus on **Continuous Compliance**. In a large cloud, how do you know if your resources follow the rules? We will use **AWS Config**, **Security Hub**, and **Trusted Advisor**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the concept of **Continuous Compliance**.
* Set up **AWS Config Rules** to enforce policies (e.g., "S3 Buckets must be private").
* Use **Security Hub** for a centralized security view.
* Analyze recommendations from **Trusted Advisor**.
* Compare Reactive vs Proactive compliance.

---

## Tools Used

* **AWS Config**
* **AWS Security Hub**
* **AWS Trusted Advisor**
* **AWS CloudTrail** (for auditing)

---

## Key Concepts

### 1. AWS Config
Records the configuration history of your resources. It asks "What changed?" and "Is it compliant?".
*   **Config Rule**: "Is port 22 open to the world?" If yes, mark as NON-COMPLIANT.
*   **Remediation**: Automatically close port 22 if detected.

### 2. AWS Security Hub
Aggregates alerts (Findings) from multiple services (GuardDuty, Inspector, Macie) into a single dashboard. It checks your account against standards like **CIS AWS Foundations Benchmark** or **PCI DSS**.

### 3. Trusted Advisor
Your personal cloud expert. It scans your account and gives recommendations in 5 categories:
*   **Cost Optimization**
*   **Performance**
*   **Security**
*   **Fault Tolerance**
*   **Service Limits**

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Config Rule** | `s3-bucket-public-read-prohibited` checks if any bucket is public. |
| **Security Standard** | Enabling **CIS Benchmark Level 1** in Security Hub. |
| **Trusted Advisor** | Checking for "Idle Load Balancers" to save money. |

---

## Bonus (Extra Learning)

*   Create a custom Config Rule using **Lambda** (e.g., "Every EC2 instance must have a `CostCenter` tag").
*   Explore **AWS Audit Manager** for automated evidence collection.

---

## Congratulations!

You’ve automated your governance! Instead of manually auditing resources once a year, you now have compliance as code running 24/7.

---

## Try These Next

*   Set up an **SNS Notification** when a resource becomes Non-Compliant.
*   Use **AWS Organizations** to apply Config Rules across multiple accounts.
