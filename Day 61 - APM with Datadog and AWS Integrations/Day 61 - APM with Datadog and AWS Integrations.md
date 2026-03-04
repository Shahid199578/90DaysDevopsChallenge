# Day 61 - APM with Datadog and AWS Integrations

Welcome to **Day 61** of the DevOps 90-Day Challenge!
Today, we dive into **APM (Application Performance Monitoring)**. Sometimes logs and metrics aren't enough—you need to see exactly *where* in the code your application is slow. We will use **Datadog**, a leading observability platform.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the difference between Infrastructure Monitoring and APM.
* Install the **Datadog Agent** on AWS EC2.
* Instrument a Python/Node.js app to send Traces to Datadog.
* Integrate Datadog with **AWS CloudWatch** to pull metrics.
* Create a **Service Map** to visualize dependencies.

---

## Tools Used

* **Datadog** (SaaS Platform)
* **Datadog Agent**
* **AWS EC2**
* **Python** (Sample App)

---

## Key Concepts

### 1. What is APM?
Application Performance Monitoring tells you:
*   **Latency**: How long did the request take?
*   **Throughput**: How many requests per second?
*   **Errors**: What percentage of requests failed?
*   **Saturation**: How full is the queue?
This is often called the **RED Method** (Rate, Errors, Duration).

### 2. The Datadog Agent
A lightweight software installed on your hosts (EC2, Kubernetes Nodes). It collects metrics (CPU/RAM) and acts as a local proxy for Traces sent by your application code.

### 3. AWS Integration
Datadog can pull metrics from AWS CloudWatch API (e.g., RDS CPU, Lambda Duration) so you can see your AWS metrics side-by-side with your application traces.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Flame Graph** | A visual breakdown of a request showing that 80% of time was spent in a MySQL query. |
| **Tagging** | Adding `env:production` and `service:payment-api` tags to filter data easily. |
| **Monitors** | Creating an alert if `p95 latency > 200ms` for 5 minutes. |

---

## Bonus (Extra Learning)

*   Set up **Datadog Log Management** to correlate logs with traces (click a trace, see the logs for that exact request).
*   Explore **Synthetic Monitoring** to ping your API from around the world.

---

## Congratulations!

You now have enterprise-grade visibility into your application stack. Datadog is a standard tool in many large organizations, so this is a highly employable skill.

---

## Try These Next

*   Enable **Database Monitoring** to see which SQL queries are the slowest.
*   Create a custom Dashboard combining EC2 CPU, RDS Connections, and API Latency.
