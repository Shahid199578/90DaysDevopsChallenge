# Day 52 - Writing Lambda Functions and Triggers (S3, API Gateway)

Welcome to **Day 52** of the DevOps 90-Day Challenge!
Today, we make our Lambda functions useful by connecting them to **Triggers**. A function that runs by itself is boring; a function that runs when something happens is magic.

[![](https://img.youtube.com/vi/AFn6w0TMjKo/0.jpg)](https://www.youtube.com/watch?v=AFn6w0TMjKo)

[Watch the video](https://www.youtube.com/watch?v=AFn6w0TMjKo)

---

## Objective

By the end of this session, you will:

* Trigger a Lambda function when a file is uploaded to **S3**.
* Trigger a Lambda function via an HTTP request using **API Gateway**.
* Inspect the **Event Object** to understand how data is passed.

---

## Tools Used

* **AWS Lambda**
* **Amazon S3** (Simple Storage Service)
* **Amazon API Gateway**

---

## Key Concepts

### 1. Triggers

A trigger is a resource or configuration that invokes your Lambda function.
* **S3 Event**: "New file created in Bucket X".
* **API Gateway**: "GET request to /users".

### 2. The S3 Trigger Flow

1. User uploads `image.jpg` to S3.
2. S3 detects the `ObjectCreated` event.
3. S3 invokes the specific Lambda Function.
4. Lambda processes the image (e.g., resizes it).

### 3. API Gateway

API Gateway acts as the "front door" for your applications. It accepts HTTP requests and passes them to the backend (Lambda).

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Event Source** | S3 Bucket or API Gateway Endpoint. |
| **Integration** | Connecting API Gateway to a Lambda function. |
| **Permissions** | Automatically granting S3 permission to invoke Lambda. |

---

## Bonus (Extra Learning)

* Print the `event` object in your Python code (`print(event)`) and check CloudWatch Logs to see the JSON structure.
* Secure your API Gateway using an **API Key**.

---

## Congratulations!

You’ve successfully built an **Event-Driven Application**!
Your code now reacts to the outside world.

---

## Try These Next

* Create a "Thumbnail Generator": Upload an image to S3, and have Lambda resize it.
* specific a **DynamoDB** trigger that runs when a new item is added to a table.
