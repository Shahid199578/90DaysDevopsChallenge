# Day 66 - Cost Optimization Strategies

Welcome to **Day 66** of the DevOps 90-Day Challenge!
Today, we tackle the biggest pain point in cloud: **Cost**. It's easy to spin up resources; it's hard to turn them off. We will learn proven strategies to reduce your AWS bill without sacrificing performance.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Identify **Unused Resources** (Zombie EC2s, Unattached EBS).
* Understand pricing models: **On-Demand vs Reserved vs Spot**.
* Implement **Rightsizing** (moving from `m5.large` to `t3.medium`).
* Use **Cost Allocation Tags** to track spend by project.
* Set up **Budgets** and Alerts.

---

## Tools Used

* **AWS Cost Explorer**
* **AWS Budgets**
* **Compute Optimizer**
* **Trusted Advisor**

---

## Key Concepts

### 1. Pricing Models
*   **On-Demand**: Pay by the second. Use for spiky workloads. Most expensive.
*   **Savings Plans / Reserved Instances (RIs)**: Commit to usage for 1 or 3 years. Save up to 72%. Use for steady-state workloads (Databases).
*   **Spot Instances**: Bid on unused capacity. Save up to 90%. Use for fault-tolerant workloads (Batch jobs, CI/CD).

### 2. Identifying Waste
*   **EBS Volumes**: Delete "Available" volumes that are not attached to any instance.
*   **Snapshots**: Delete old snapshots.
*   **Elastic IPs**: Release unassociated EIPs (you pay for them if you don't use them!).
*   **Load Balancers**: Delete idle ALBs.

### 3. Rightsizing
AWS Compute Optimizer analyzes your CPU/RAM metrics and recommends instance types. "You are using `c5.xlarge` but your CPU is 5%. Switch to `t3.medium` to save $100/month."

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Tagging Strategy** | Tagging every resource with `Owner: AnalyticsTeam`. |
| **Spot Fleet** | Using Spot Instances for Jenkins Agents. |
| **Lifecycle Policies** | Moving S3 objects to **Glacier** after 90 days. |

---

## Bonus (Extra Learning)

*   Set up an **AWS Budget** that emails you if your bill exceeds $10.
*   Use **AWS Instance Scheduler** to turn off Dev environments at night (7 PM - 7 AM).

---

## Congratulations!

You’ve learned how to save money! In the real world, this skill makes you a hero to the CFO. Cloud cost optimization (FinOps) is a critical DevOps responsibility.

---

## Try These Next

*   Analyze your bill in Cost Explorer grouping by **Service** and **Region**.
*   Purchase a **Convertible Reserved Instance** (simulated).
