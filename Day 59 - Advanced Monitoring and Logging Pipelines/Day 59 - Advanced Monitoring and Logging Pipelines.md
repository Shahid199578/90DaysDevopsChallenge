# Day 59 - Advanced Monitoring and Logging Pipelines

Welcome to **Day 59** of the DevOps 90-Day Challenge!
Today we scale up our observability. Viewing logs in the console is fine for one server, but what about 1,000? We will build **Advanced Logging Pipelines** using Kinesis and OpenSearch.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Move beyond "SSH and grep".
* Build a Centralized Logging Architecture.
* Stream logs from **CloudWatch** to **OpenSearch (Elasticsearch)**.
* Use **Kinesis Data Firehose** for buffering and delivery.
* Create a **Kibana Dashboard** to visualize error rates.

---

## Tools Used

* **Amazon CloudWatch**
* **Amazon Kinesis Data Firehose**
* **Amazon OpenSearch Service** (formerly Elasticsearch)
* **Kibana**

---

## Key Concepts

### 1. The ELK/EFK Stack on AWS
*   **Elasticsearch (OpenSearch)**: The search engine / database for logs.
*   **Logstash (or Firehose)**: The ingestion pipeline.
*   **Kibana**: The visualization UI.

### 2. Subscription Filters
You can attach a **Subscription Filter** to a CloudWatch Log Group. This tells CloudWatch: "Don't just keep this log here—stream it immediately to Kinesis/Lambda!"

### 3. Why Kinesis?
Directly streaming to Elasticsearch can overwhelm it during traffic spikes. **Kinesis** acts as a buffer/queue, handling the high throughput and writing to ES in bulk.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Centralization** | Aggregating logs from APIGateway, Lambda, and EC2 into one dashboard. |
| **Real-Time Analysis** | Seeing errors appear in Kibana seconds after they happen. |
| **S3 Backup** | Configuring Firehose to dump a raw backup of all logs to S3 "just in case". |

---

## Bonus (Extra Learning)

*   Create a dashboard in Kibana showing "Top 10 API 404 Errors".
*   Explore **Prometheus** and **Grafana** as an alternative to CloudWatch for metrics.

---

## Congratulations!

You have stepped into the world of **Big Data Ops**! Building logging pipelines is a key skill for SREs (Site Reliability Engineers).

---

## Try These Next

*   Send your logs to **Datadog** or **Splunk** (simulated) using Firehose.
*   Set up an alert in OpenSearch to notify Slack when critical errors spike.
