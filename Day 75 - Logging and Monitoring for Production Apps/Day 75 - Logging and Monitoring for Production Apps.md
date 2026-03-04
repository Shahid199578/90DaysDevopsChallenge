# Day 75 - Logging and Monitoring for Production Apps

Welcome to **Day 75** of the DevOps 90-Day Challenge!
We revisit observability, but this time with a focus on **Production Apps**. It's not just about installing tools; it's about what you *actually* monitor to keep the business running.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Define **SLIs** (Service Level Indicators) and **SLOs** (Service Level Objectives).
* Differentiate between **White-box** (internal metrics) and **Black-box** (uptime checks) monitoring.
* Set up **Synthetic Monitoring**.
* Create a **Runbook** for responding to alerts.

---

## Tools Used

* **CloudWatch Synthetics** (Canaries)
* **PagerDuty** (Concept)
* **Better Uptime** (or similar)

---

## Key Concepts

### 1. The Golden Signals
Google SRE book defines 4 signals you must monitor:
1.  **Latency**: Time it takes to serve a request.
2.  **Traffic**: How much demand is on your system.
3.  **Errors**: Rate of requests that fail.
4.  **Saturation**: How "full" your service is (CPU/Memory).

### 2. Synthetic Monitoring
A script that simulates a user. It logs in, clicks a button, and expects a result. If it fails, you know the *user experience* is broken, even if your server CPU is low.

### 3. Alert Fatigue
Don't alert on everything. Alert only if a human needs to wake up.
*   Good Alert: "Checkout page is returning 500s."
*   Bad Alert: "Server CPU is 80%." (Who cares? Autoscaling handles this).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Canary** | A script running every minute to ping the `/health` endpoint. |
| **SLO** | "99.9% of requests must be faster than 300ms." |
| **Error Budget** | "We can afford 43 minutes of downtime per month." |

---

## Bonus (Extra Learning)

*   Write a Python script that checks your website status and sends a Discord message if down.
*   Read the **Google SRE Book** (Configuring Monitoring chapter).

---

## Congratulations!

You are learning to think like a Site Reliability Engineer (SRE). Monitoring is the foundation of reliability.

---

## Try These Next

*   Implement a dashboard that shows the "Golden Signals" for your application.
*   Simulate an outage and measure your **MTTR** (Mean Time To Recovery).
