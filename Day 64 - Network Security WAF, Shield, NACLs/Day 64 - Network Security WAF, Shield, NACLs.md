# Day 64 - Network Security: WAF, Shield, NACLs

Welcome to **Day 64** of the DevOps 90-Day Challenge!
Today, we focus on **Network Security**. It's not enough to lock the door (IAM); you also need a fence around the house. We will explore **WAF** (Web Application Firewall), **Shield**, and **NACLs**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Protect your web apps from common attacks (SQL Injection, XSS) using **AWS WAF**.
* Understand **DDoS Protection** with **AWS Shield**.
* Configure **Network ACLs** for subnet-level security.
* Compare **Security Groups** vs **NACLs**.

---

## Tools Used

* **AWS WAF**
* **AWS Shield** (Standard vs Advanced)
* **VPC** (NACLs & Security Groups)

---

## Key Concepts

### 1. AWS WAF
A firewall that inspects HTTP/HTTPS traffic. You attach it to CloudFront, ALB, or API Gateway.
*   **Rules**: "Block requests from IP 1.2.3.4" or "Block requests containing `SELECT * FROM`".
*   **Managed Rules**: Pre-configured rulesets from AWS (e.g., OWASP Top 10).

### 2. AWS Shield
*   **Standard**: Free. Protects against common L3/L4 DDoS attacks (SYN floods). Automatically enabled.
*   **Advanced**: Paid ($3k/month). Protects against sophisticated attacks and provides access to the DDoS Response Team (DRT).

### 3. NACL vs Security Group
*   **Security Group**: Stateful. Applied to Instance. Allow rules only.
*   **NACL**: Stateless. Applied to Subnet. Allow **and Deny** rules. (Use this to block specific IPs).

---

## Key Concepts Applied

| Concept | Application |
| :--- | :--- |
| **IP Set** | Creating a list of "Bad IPs" and blocking them in WAF. |
| **Rate Limiting** | Blocking any IP that sends more than 100 requests in 5 minutes. |
| **Subnet Isolation** | Using NACLs to prevent the Database Subnet from accessing the Internet directly. |

---

## Bonus (Extra Learning)

*   Simulate an **SQL Injection** attack on your test app and watch WAF block it.
*   Enable **WAF Logging** to analyze blocked requests in CloudWatch Logs.

---

## Congratulations!

You’ve built a fortress around your application! Network security is the first line of defense against external threats.

---

## Try These Next

*   Deploy a **Honeypot** using WAF triggers (if someone hits `/admin.php`, block their IP).
*   Review your VPC Flow Logs to see accepted/rejected traffic.
