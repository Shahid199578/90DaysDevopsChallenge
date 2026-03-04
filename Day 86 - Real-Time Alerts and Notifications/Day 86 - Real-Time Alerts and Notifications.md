# Day 86 - Real-Time Alerts and Notifications

Welcome to **Day 86** of the DevOps 90-Day Challenge!
Dashboards are for looking; Alerts are for acting. Today we set up an **Alerting Strategy** that wakes you up when it matters (and lets you sleep when it doesn't).

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Integrate **CloudWatch Alarms** with **SNS**.
* Send alerts to **Email**, **Slack**, and **PagerDuty** (or mobile SMS).
* Create **Composite Alarms** (Alarm A AND Alarm B).
* Classify alerts by severity (Info, Warning, Critical).

---

## Tools Used

* **Amazon SNS**
* **AWS CloudWatch**
* **AWS Chatbot** (for Slack integration)
* **Lambda** (for custom notifications)

---

## Key Concepts

### 1. The Notification Pipeline
Metric (CPU > 90%) -> CloudWatch Alarm -> SNS Topic -> AWS Chatbot -> Slack Channel.

### 2. Severity Levels
*   **P1 (Critical)**: Site is down. Wake up the on-call engineer immediately (PagerDuty/Call).
*   **P2 (Warning)**: High latency or low disk space. Fix it during business hours (Jira Ticket/Email).
*   **P3 (Info)**: Deployment successful. Just a log (Slack).

### 3. AWS Chatbot
A native service that pushes alerts to Slack/Teams. It also allows you to run commands from Slack (`@aws lambda invoke...`) - ChatOps!

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Deduplication** | Understanding that PagerDuty/OpsGenie handles grouping similar alerts so you don't get 1000 calls. |
| **Escalation Policy** | If Engineer A doesn't ack in 15 mins, call Engineer B. |
| **Rich Messages** | Formatting the alert to include a link to the relevant Runbook. |

---

## Bonus (Extra Learning)

*   Write a Lambda function that receives an SNS alert and automatically reboots the failed EC2 instance (Self-Healing).
*   Set up a "Dead Man's Switch" (Heartbeat) alert.

---

## Congratulations!

You are now connected to the pulse of your infrastructure.

---

## Try These Next

*   Implement **Prometheus Alertmanager** logic.
*   Route alerts based on tags (Team A alerts go to Team A channel).
