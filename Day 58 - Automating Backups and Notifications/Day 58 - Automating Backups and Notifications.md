# Day 58 - Automating Backups and Notifications

Welcome to **Day 58** of the DevOps 90-Day Challenge!
Data is the most valuable asset in any organization. Today, we learn how to **automate backups** and set up notifications to ensure you never lose data and are always informed of system health.

[![](https://img.youtube.com/vi/J3u5KsIrmx4/0.jpg)](https://www.youtube.com/watch?v=J3u5KsIrmx4)


[Watch the video](https://www.youtube.com/watch?v=J3u5KsIrmx4)  

---

## Objective

By the end of this session, you will:

* Understand the importance of **Disaster Recovery (DR)**.
* Automate **EBS Snapshots** using Data Lifecycle Manager (DLM).
* Automate **RDS Backups** and configure retention.
* Use **AWS Backup** for centralized compliance.
* Set up **SNS Alerts** for backup failures.

---

## Tools Used

* **Amazon EC2 (EBS)**
* **Amazon RDS**
* **AWS Backup**
* **Amazon Data Lifecycle Manager (DLM)**
* **Amazon SNS**

---

## Key Concepts

### 1. Snapshot vs Backup
*   **EBS Snapshot**: A point-in-time copy of your disk volume. First snapshot is full; subsequent ones are incremental (only changes are saved).
*   **AWS Backup**: A managed service that orchestrates backups across EC2, RDS, DynamoDB, EFS, and more from a single console.

### 2. Recovery Point Objective (RPO)
"How much data can we afford to lose?"
If you backup every 24 hours, your RPO is 24 hours.

### 3. Recovery Time Objective (RTO)
"How long does it take to restore?"
If it takes 4 hours to restore the database from a snapshot, your RTO is 4 hours.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Lifecycle Policy** | "Take a snapshot every 12 hours, keep for 7 days." |
| **Cross-Region Copy** | Automatically copying backups to `us-west-1` for disaster recovery. |
| **SNS Topic** | `Backup-Alerts` topic that emails admins if a job fails. |

---

## Bonus (Extra Learning)

*   Restore an EC2 instance from a snapshot you just created.
*   Enable **Backup Vault Lock** to prevent anyone (even root!) from deleting backups for a set period (WORM compliance).

---

## Congratulations!

You’ve properly protected your infrastructure. Automation isn't just about deploying code; it's about **protecting** what you've deployed.

---

## Try These Next

*   Simulate a "database failure" and restore your RDS instance to a new endpoint.
*   Write a Lambda function that deletes snapshots older than 30 days (manual cleanup vs DLM).
