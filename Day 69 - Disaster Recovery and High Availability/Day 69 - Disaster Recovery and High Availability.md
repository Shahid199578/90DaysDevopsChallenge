# Day 69 - Disaster Recovery and High Availability

Welcome to **Day 69** of the DevOps 90-Day Challenge!
Today, we talk about resilience. **High Availability (HA)** keeps you running when a server fails. **Disaster Recovery (DR)** brings you back when an entire Region fails.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand **RPO** (Recovery Point Objective) and **RTO** (Recovery Time Objective).
* Design an HA architecture using **Multi-AZ**.
* Implement DR strategies: **Backup & Restore**, **Pilot Light**, **Warm Standby**, and **Multi-Site**.
* Use **Route 53 Failover Routing** to switch traffic between regions.

---

## Tools Used

* **Amazon Route 53**
* **Elastic Load Balancer (ELB)**
* **Auto Scaling Groups (ASG)**
* **RDS Multi-AZ**
* **S3 Cross-Region Replication**

---

## Key Concepts

### 1. High Availability (HA)
Availability is measured in "nines".
*   99.9% = 8.7 hours downtime/year.
*   99.999% = 5 minutes downtime/year.
Achieved by eliminating **Single Points of Failure (SPOF)**.
*   *Component Redundancy*: Redundant power supplies.
*   *Geographic Redundancy*: Deploying across multiple Availability Zones (AZs).

### 2. DR Strategies
1.  **Backup & Restore**: Cheapest, slowest (High RTO). Restore form S3 backups.
2.  **Pilot Light**: Core services (DB) running in DR region, but app servers are off. Start them only during disaster.
3.  **Warm Standby**: Scaled-down version running in DR region. Scale up during disaster.
4.  **Multi-Site Active/Active**: Expensive, zero downtime. Both regions serve traffic.

### 3. Route 53 Health Checks
Route 53 monitors your endpoint (`us-east-1`). If it returns 500 or times out, Route 53 updates DNS to point to the DR region (`us-west-2`).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Active/Passive** | Primary DB in us-east-1 (Active), Replicas in us-east-2 (Passive, waiting). |
| **Failover Testing** | Manually "breaking" the primary server to see if the secondary takes over. |
| **Data Replication** | Enabling S3 Cross-Region Replication (CRR) for critical buckets. |

---

## Bonus (Extra Learning)

*   Calculate the cost difference between **Pilot Light** and **Warm Standby** for your stack.
*   Use **AWS Chaos Engineering** (Fault Injection Service) to simulate an AZ outage.

---

## Congratulations!

You now know how to design systems that survive the apocalypse (or just a power outage). Resilience is a key differentiator for Senior DevOps Engineers.

---

## Try These Next

*   Set up a simple static website in S3 in two regions and configure Route 53 Failover.
*   Read the **AWS Well-Architected Framework** Reliability Pillar.
