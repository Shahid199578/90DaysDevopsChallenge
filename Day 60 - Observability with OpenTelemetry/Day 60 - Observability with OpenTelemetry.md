# Day 60 - Observability with OpenTelemetry

Welcome to **Day 60** of the DevOps 90-Day Challenge!
Today, we explore the modern standard for observability: **OpenTelemetry (OTel)**. Gone are the days of proprietary agents for every tool. OTel provides a unified way to collect traces, metrics, and logs.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the "Three Pillars of Observability": **Metrics**, **Logs**, and **Traces**.
* Learn what **OpenTelemetry** is and why it's the future.
* Instrument a simple Python/Node.js app to send Traces.
* connect OTel to a backend like **Jaeger** or **Prometheus**.

---

## Tools Used

* **OpenTelemetry SDK**
* **Jaeger** (Tracing Backend)
* **Docker** (to run Jaeger locally)
* **Python** (Sample App)

---

## Key Concepts

### 1. Monitoring vs Observability
*   **Monitoring**: "Is the system healthy?" (Yes/No). Dashboard tells you consumption is high.
*   **Observability**: "Why is the system behaving this way?" (Debugging). Traces tell you *which* database query caused the consumption spike.

### 2. Distributed Tracing
In microservices, a single user request hits 10 different services. A **Trace** tracks that request across all of them using a unique **Trace ID**.
*   **Span**: A single unit of work (e.g., "Query Database", "Call Payment API").

### 3. The Collector
The **OTel Collector** allows you to receive data in one format and export it to multiple backends (Jaeger, Datadog, New Relic) without changing your application code.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Instrumentation** | Adding code (`tracer.start_span`) to measure function duration. |
| **Context Propagation** | Passing the Trace ID from Service A to Service B via HTTP Headers. |
| **Exporters** | Sending the collected data to the Jaeger UI for visualization. |

---

## Bonus (Extra Learning)

*   Run Jaeger using Docker Compose: `docker run -d -p 16686:16686 jaegertracing/all-in-one`.
*   Explore **Auto-Instrumentation** agents that trace your code without you writing a single line.

---

## Congratulations!

You’ve reached the 60-Day mark! You are now dealing with advanced reliability engineering concepts. Observability is what separates "Developers" from "DevOps Engineers".

---

## Try These Next

*   Instrument a frontend application (React/Angular) to see user latency.
*   Connect OpenTelemetry to AWS X-Ray.
