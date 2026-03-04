# Day 77 - Automating EC2/Container Backups

Welcome to **Day 77** of the DevOps 90-Day Challenge!
We previously covered backups in general (Day 70). Today, we get specific: How do you back up **Kubernetes**? Snapshots aren't enough when you have stateful pods. We also revisit EC2 automation.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Install **Velero** for Kubernetes backups.
* Back up a specific **Namespace** to S3.
* Restore a deleted namespace (Crash Recovery).
* Automate EC2 AMI creation using **Systems Manager (SSM)**.

---

## Tools Used

* **Velero** (K8s Backup)
* **AWS S3**
* **AWS Systems Manager**

---

## Key Concepts

### 1. The Kubernetes Backup Problem
Backing up the etcd database is hard. Backing up the PV (EBS volume) is easy, but you lose the YAML configuration (Deployments, Services).
**Velero** solves this by backing up BOTH the YAML (to S3) and the Volume (Snapshot).

### 2. Velero Architecture
*   **Velero Server**: Runs in the cluster.
*   **Velero CLI**: Runs on your laptop.
*   **Object Storage**: S3 bucket where backups live.

### 3. Systems Manager Automation
Use SSM Maintenance Windows to trigger an "AMI Creation" run command across all instances tagged `PatchGroup: Prod` every Sunday at 2 AM.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Disaster Recovery** | Nuke the entire cluster. Rebuild it. Run `velero restore create --from-backup my-backup`. Watch everything come back. |
| **Migration** | Using Velero to migrate resources from Cluster A (Dev) to Cluster B (Prod). |
| **Schedules** | `velero schedule create daily --schedule="0 1 * * *"` |

---

## Bonus (Extra Learning)

*   Back up a **StatefulSet** with Persistent Volumes using Restic/Kopia integration in Velero.
*   Use SSM to run a shell script on 100 EC2 instances simultaneously.

---

## Congratulations!

You have filled the gap in your backup strategy. Kubernetes requires special care, and Velero is the industry standard tool for it.

---

## Try These Next

*   Restore a backup to a different namespace.
*   Back up only resources with the label `app=nginx`.
