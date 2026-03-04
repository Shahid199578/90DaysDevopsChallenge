# Day 81 - X-Ray for Tracing Microservices

Welcome to **Day 81** of the DevOps 90-Day Challenge!
Debugging microservices is hard. **AWS X-Ray** helps you visualize requests as they travel through your application specific to the AWS ecosystem.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand **Distributed Tracing** (Trace ID, Segments).
* Instrument a Python/Node.js app with the **X-Ray SDK**.
* Analyze the **Service Map** to find bottlenecks.
* Integrate X-Ray with **Lambda** and **API Gateway**.

---

## Tools Used

* **AWS X-Ray**
* **AWS Lambda**
* **Amazon API Gateway**
* **DynamoDB**

---

## Key Concepts

### 1. Tracing vs Logging
Logs show *events*. Traces show *request flow*.
Trace: "User hit API -> API hit Lambda -> Lambda hit DynamoDB (Slow) -> returned".
X-Ray shows you the latency of *each* hop.

### 2. The Service Map
X-Ray automatically draws a map of your architecture. You can see:
*   Which services are calling each other.
*   High latency connections (colored Yellow/Red).
*   Error rates.

### 3. Sampling
You don't need to trace 100% of requests (expensive!). You trace 5% or 1 request/sec. This gives you statistical confidence without the cost.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Annotations** | Adding custom metadata (e.g., `user_id: 123`) to the trace so you can search for it later. |
| **Integrations** | Chechkbox "Enable X-Ray" in Lambda and API Gateway settings (Zero code!). |
| **Cold Starts** | Viewing the trace to confirm if latency was due to Lambda Initialization (Cold Start) or code execution. |

---

## Bonus (Extra Learning)

*   Compare X-Ray with OpenTelemetry/Jaeger (Day 60).
*   Use X-Ray Analytics to compare "Latency of Premium Users vs Free Users".

---

## Congratulations!

You have visibility. You no longer need to guess why the API is slow. You *know*.

---

## Try These Next

*   Install the X-Ray Daemon on EC2 (Docker container) to trace EC2 apps.
*   Set up encryption for X-Ray data using KMS.
