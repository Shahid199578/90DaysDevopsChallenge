# Day 70 - Backup and Snapshot Automation

Welcome to **Day 70** of the DevOps 90-Day Challenge!
Today, we focus on **Data Protection Automation**. We touched on this in Day 58, but today we dive deeper into **Lifecycle Management** and **Cross-Region Copying** to fully satisfy DR requirements.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Master **Data Lifecycle Manager (DLM)** for EBS.
* Automate **AWS Backup** plans for EFS and DynamoDB.
* script custom backup solutions using **Lambda** and **Boto3**.
* Verify backups by performing a **Restore Drill**.

---

## Tools Used

* **Amazon Data Lifecycle Manager**
* **AWS Backup**
* **AWS Lambda** (for custom logic)
* **Amazon EventsBridge** (Scheduler)

---

## Key Concepts

### 1. Snapshot Chains
EBS Snapshots are incremental.
*   Snapshot A (10GB) -> Change 1GB -> Snapshot B (1GB).
*   Deleting Snapshot A does *not* lose data needed for Snapshot B. AWS handles the merging internally.

### 2. AWS Backup Vaults & Locks
*   **Backup Vault**: A container for your backups.
*   **Vault Lock**: Implements WORM (Write Once, Read Many). This prevents hackers (Ransomware) from deleting your backups even if they hack your root account.

### 3. Cross-Account Backup
For ultimate security, copy your backups to a completely different AWS Account (The "Bunker" Account). If your Production account is compromised, the Bunker is safe.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Tag-Based Backup** | Creating a Backup Plan that automatically backs up any resource with tag `Backup: Daily`. |
| **Point-in-Time Recovery (PITR)** | Restoring a DynamoDB table to the state it was in exactly 5 minutes ago. |
| **Retention** | Keeping daily backups for 30 days, monthly backups for 1 year, and yearly backups for 7 years. |

---

## Bonus (Extra Learning)

*   Write a script to audit if all your Prod EC2 instances are covered by a Backup Plan.
*   Set up **AWS Backup Audit Manager** to generate compliance reports.

---

## Congratulations!

Your data is safe, secure, and compliant. You have automated the most boring but important part of IT operations.

---

## Try These Next

*   Perform a restore of a 100GB volume and measure how long it takes (RTO validation).
*   Implement Cross-Account backup copying using AWS Backup.
