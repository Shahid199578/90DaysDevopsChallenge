# Day 55 - Logging with CloudWatch for Lambda

Welcome to **Day 55** of the DevOps 90-Day Challenge!
Today, we focus on **logging** in serverless applications using **AWS CloudWatch**. Logs are essential to debug, troubleshoot, and analyze the behavior of your Lambda functions and serverless workflows.

[![](https://img.youtube.com/vi/cnw4UgiRM2w/0.jpg)](https://www.youtube.com/watch?v=cnw4UgiRM2w)


[Watch the video](https://www.youtube.com/watch?v=cnw4UgiRM2w)

---

## Objective

By the end of this session, you will:

* Understand why logging is critical in serverless architectures.
* Learn how Lambda integrates natively with CloudWatch Logs.
* Write custom log statements in Python/Node.js for Lambda.
* View, filter, and analyze logs in the CloudWatch Console.
* Set up **Log Retention Policies** to manage costs.

---

## Tools Used

* **AWS Lambda** (Function execution)
* **Amazon CloudWatch Logs** (Log storage and analysis)
* **AWS IAM** (Permissions for logging)
* **Python/Boto3** (Runtime)

---

## Key Concepts

### 1. The Need for Logging
In a traditional server, you might SSH in and check `/var/log/syslog`. In Lambda, there is no persistent server. All output (`stdout`/`stderr`) is automatically captured by the execution environment and sent to CloudWatch Logs.

### 2. Log Groups and Streams
*   **Log Group**: A collection of log streams that share the same retention, monitoring, and access control settings. Lambda creates a group named `/aws/lambda/<function-name>`.
*   **Log Stream**: A sequence of log events that share the same source (a specific Lambda container instance).

### 3. Writing Logs
Simply printing to standard output works!

**Python:**
```python
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    logger.info("Function started execution")
    print("This also goes to CloudWatch")
    return "Done"
```

---

## Key Concepts Applied

| Concept | Description |
| :--- | :--- |
| **Structured Logging** | Writing logs in JSON format for easier parsing and querying. |
| **Log Retention** | Configuring logs to expire after X days (e.g., 7 days) to save storage costs. |
| **CloudWatch Insights** | Using query syntax to search through millions of log lines instantly. |

---

## Bonus (Extra Learning)

*   Explore **CloudWatch Log Insights** to run SQL-like queries on your logs.
*   Create a **Metric Filter** to count occurrences of the word "ERROR" in your logs.

---

## Congratulations!

You now have visibility into your Serverless functions! Without logs, a Lambda function is a black box. Now it's a transparent, debuggable unit of work.

---

## Try These Next

*   Intentionally raise an error in your Lambda and find the **Stack Trace** in CloudWatch.
*   Export your logs to **Amazon S3** for long-term archiving.
