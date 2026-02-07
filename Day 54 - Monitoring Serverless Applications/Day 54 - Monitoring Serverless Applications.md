# Day 54 - Monitoring Serverless Applications

Welcome to **Day 54** of the DevOps 90-Day Challenge!
Today, we focus on **Operational Visibility**: Monitoring. Since you cannot SSH into a Lambda function, you need robust tools to know if your application is healthy.

[![](https://img.youtube.com/vi/-GljcEP5PgM/0.jpg)](https://www.youtube.com/watch?v=-GljcEP5PgM)

[Watch the video](https://www.youtube.com/watch?v=-GljcEP5PgM)

---

## Objective

By the end of this session, you will:

* Monitor Lambda functions using **Amazon CloudWatch**.
* Analyze logs to debug errors.
* Use **AWS X-Ray** to trace requests through your distributed application.

---

## Tools Used

* **Amazon CloudWatch** (Logs & Metrics)
* **AWS X-Ray** (Distributed Tracing)
* **AWS Lambda**

---

## Key Concepts

### 1. CloudWatch Logs

Every time your Lambda prints something (`print("hello")`), it goes to a **CloudWatch Log Group**. This is where you look when things go wrong.

### 2. CloudWatch Metrics

* **Invocations**: How many times was it run?
* **Duration**: How long did it take? (Money!)
* **Errors**: How many times did it crash?
* **Throttles**: Did you hit the concurrency limit?

### 3. AWS X-Ray

X-Ray provides a "Service Map". It shows you a visual graph of your application.
User -> API Gateway -> Lambda -> DynamoDB
It helps you spot **Latency** (where is it slow?) and **Errors** (where is it failing?).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Observability** | Understanding the internal state based on outputs (logs/metrics). |
| **Tracing** | Following a single request across multiple services. |
| **Alarms** | Setting up a notification if `Errors > 0`. |

---

## Bonus (Extra Learning)

* Create a **CloudWatch Alarm** that sends an email (SNS) if your function errors out.
* specific **Structured Logging** (JSON) for easier searching.

---

## Congratulations!

You’ve successfully learned how to **Monitor and Debug** Serverless applications!
You have now completed the Serverless section of the challenge.

---

## Try These Next

* Build a custom **CloudWatch Dashboard** for your Serverless App.
* Look into third-party monitoring tools like **Datadog** or **New Relic** for Serverless.
