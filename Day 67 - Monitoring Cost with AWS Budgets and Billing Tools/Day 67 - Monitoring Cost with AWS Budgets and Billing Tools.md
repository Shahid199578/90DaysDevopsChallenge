# Day 67 - Monitoring Cost with AWS Budgets and Billing Tools

Welcome to **Day 67** of the DevOps 90-Day Challenge!
Today, we dive into **Billing Visibility**. If you don't know *where* your money is going, you can't save it. We will learn to use **AWS Budgets**, **Cost Explorer**, and **Cost and Usage Reports (CUR)**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Create an **AWS Budget** to track your monthly spend.
* Set up **Cost Alerts** (e.g., "Alert me if forecasted cost > $50").
* Use **Cost Explorer** to visualize spending trends.
* Export detailed billing data using **CUR**.

---

## Tools Used

* **AWS Budgets**
* **AWS Cost Explorer**
* **AWS Billing Console**

---

## Key Concepts

### 1. AWS Budgets vs Cost Explorer
*   **Cost Explorer**: Interactive tool for historical analysis and forecasting. "How much did I spend last month on EC2?"
*   **Budgets**: Proactive monitoring. "Tell me *before* I spend too much."

### 2. Types of Budgets
*   **Cost Budget**: Based on dollar amount.
*   **Usage Budget**: Based on usage (e.g., "Alert if EC2 runs > 1000 hours").
*   **Reservation Budget**: Tracking RI or Savings Plan utilization.

### 3. Forecasting
AWS uses machine learning to predict your end-of-month bill based on current usage. You can set alarms on *forecasted* costs, not just actual costs.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Alert Threshold** | Creating an email alert at 80% ($80) and 100% ($100) of the budget. |
| **Granularity** | Checking daily vs monthly spend to spot spikes. |
| **Filtering** | Filtering costs by `Region: us-east-1` or `Service: Amazon RDS`. |

---

## Bonus (Extra Learning)

*   Enable **Hourly Granularity** in Cost Explorer (Warning: costs extra!).
*   Set up a **Budget Action** to automatically stop EC2 instances if budget is exceeded (requires IAM permissions).

---

## Congratulations!

You’ve set up your financial guardrails! No more surprise bills at the end of the month. You are now in full control of your cloud spending.

---

## Try These Next

*   Create a report grouping costs by **Instance Type**.
*   Download your invoice as a PDF and understand the line items.
