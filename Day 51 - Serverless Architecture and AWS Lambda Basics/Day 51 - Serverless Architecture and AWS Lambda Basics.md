# Day 51 - Serverless Architecture and AWS Lambda Basics

Welcome to **Day 51** of the DevOps 90-Day Challenge!
Today, we start our journey into **Serverless Computing**, exploring the architecture where you build and run applications without thinking about servers.

[![](https://img.youtube.com/vi/knoOcF525sw/0.jpg)](https://www.youtube.com/watch?v=knoOcF525sw)

[Watch the video](https://www.youtube.com/watch?v=knoOcF525sw)

---

## Objective

By the end of this session, you will:

* Understand what **Serverless** means (and what it doesn't).
* Create your first **AWS Lambda** function.
* Execute code in the cloud without provisioning a single EC2 instance.

---

## Tools Used

* **AWS Console**
* **AWS Lambda**
* **Python** (for the function code)

---

## Key Concepts

### 1. What is Serverless?

Serverless doesn't mean "no servers". It means **you don't manage the servers**. AWS handles the infrastructure, scaling, and patching. You just focus on the code.

**Benefits:**
* **Pay-per-use**: You only pay for the compute time you consume.
* **Auto-scaling**: Scales from zero to thousands of requests automatically.
* **No Ops**: Zero infrastructure management.

### 2. AWS Lambda

Lambda is an event-driven compute service. It runs your code in response to events (like a file upload, an HTTP request, or a timer).

**Basic Lambda Structure (Python):**

```python
import json

def lambda_handler(event, context):
    print("Function started...")
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **FaaS** | Function-as-a-Service (running `lambda_handler`). |
| **Event Object** | JSON data passed to the function containing trigger details. |
| **Cold Start** | The slight delay when a function is invoked for the first time. |

---

## Bonus (Extra Learning)

* Compare **Lambda** vs **EC2** pricing for a small API.
* Explore **AWS Fargate** for serverless containers.

---

## Congratulations!

You’ve successfully entered the world of **Serverless**!
You just ran code in the cloud without booting up a server. That's powerful.

---

## Try These Next

* Change the runtime to **Node.js** and write a "Hello World" function.
* Try to invoke the function using the **AWS CLI**.
