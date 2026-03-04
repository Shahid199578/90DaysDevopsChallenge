# Day 85 - High Availability Setup on AWS

Welcome to **Day 85** of the DevOps 90-Day Challenge!
We touched on HA before, but today we implement a full **Multi-Tier HA Architecture**. This is the standard architecture for any serious application.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Architect a **3-Tier Application** (Web, App, DB).
* Deploy across **Multiple Availability Zones (Multi-AZ)**.
* Configure **Application Load Balancers (ALB)** and **Auto Scaling Groups (ASG)**.
* Set up **RDS Multi-AZ** for database failover.

---

## Tools Used

* **AWS VPC**
* **AWS EC2 / ASG**
* **AWS ALB**
* **Amazon RDS**

---

## Key Concepts

### 1. The 3-Tier Architecture
*   **Public Subnet**: Load Balancer (Internet facing).
*   **Private Subnet 1**: Web/App Servers (ASG). No direct internet access.
*   **Private Subnet 2**: Database (RDS). Highly secured.

### 2. Multi-AZ Redundancy
Deploying 2 Web Servers: One in `us-east-1a`, one in `us-east-1b`. If AZ 'a' burns down, AZ 'b' keeps running.
The Load Balancer health checks will automatically stop sending traffic to the dead AZ.

### 3. Database HA
RDS Primary is in AZ 'a'. Standby is in AZ 'b'. Data is synchronously replicated. If Primary fails, AWS flips the DNS to Standby automatically (Failover).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Security Groups** | Chaining SG: LB allows port 80 -> Web allows port 80 from LB -> DB allows port 3306 from Web. |
| **NAT Gateway** | Allowing private servers to download yum updates without exposing them to incoming internet traffic. |
| **Session Stickiness** | Configuring ALB to keep a user on the same server (if needed) or using Redis for session storage (Better). |

---

## Bonus (Extra Learning)

*   Simulate an AZ failure by modifying the NACL to block all traffic to Subnet A.
*   Move static assets to **CloudFront** (CDN) to offload the web servers.

---

## Congratulations!

You have built a robust, enterprise-grade architecture. This is exactly how companies like Netflix and Amazon architect for uptime.

---

## Try These Next

*   Add **ElastiCache** (Redis) to the architecture.
*   Automate this entire setup with Terraform modules.
