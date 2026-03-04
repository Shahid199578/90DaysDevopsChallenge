# Day 76 - Real-Time Dashboards with Grafana + Loki

Welcome to **Day 76** of the DevOps 90-Day Challenge!
Metrics (Grafana) tell you *that* something is wrong. Logs (Loki) tell you *why*. Today we integrate **Loki**, the "Prometheus for Logs".

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Install **Loki** and **Promtail** (Log collector).
* Connect Loki to **Grafana** as a data source.
* Query logs using **LogQL** (Loki Query Language).
* Build a dashboard that correlates Metrics and Logs (Split view).

---

## Tools Used

* **Grafana Loki**
* **Promtail**
* **Grafana**
* **Docker/Kubernetes**

---

## Key Concepts

### 1. What is Loki?
Unlike ELK, Loki does *not* index the text of the logs. It only indexes the **labels** (metadata). This makes it widely cheaper and faster to ingest. It's like `grep` for the cloud.

### 2. Promtail
The agent that runs on your nodes (like Fluent Bit). It tails the log files, attaches labels (pod name, namespace), and pushes to Loki.

### 3. LogQL
The query language.
*   `{app="frontend"}`: Select logs for frontend.
*   `{app="frontend"} |= "error"`: Grep for "error".
*   `rate({app="frontend"} |= "error" [5m])`: Calculate the rate of errors over time (Transforming logs into metrics!).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Labeling** | Ensuring logs carry `env=production` so we can filter them easily. |
| **Correlation** | Clicking a spike in the CPU graph and seeing the logs from that exact timeframe. |
| **Visualizing Logs** | creating a "Logs Volume" graph to see if your app suddenly started spamming logs. |

---

## Bonus (Extra Learning)

*   Set up an alert in Grafana based on a Loki query ("Alert if keyword 'Exception' appears > 10 times in 1 min").
*   Use **Grafana Cloud** free tier to test Loki.

---

## Congratulations!

You now have a modern, lightweight logging stack. The "PLG Stack" (Prometheus, Loki, Grafana) is the gold standard for many DevOps teams.

---

## Try These Next

*   Parse a JSON log line in LogQL (`| json`).
*   Explore **Grafana Tempo** for Tracing (completing the trio).
