# Day 56 - Real-World Serverless Automation Example

Welcome to **Day 56** of the DevOps 90-Day Challenge!
Today, we bring everything together by exploring a **real-world serverless automation project**. We will build a pipeline that processes files automatically when uploaded to S3.


[![](https://img.youtube.com/vi/l8I6n4acAi8/0.jpg)](https://www.youtube.com/watch?v=l8I6n4acAi8)


[Watch the video](https://www.youtube.com/watch?v=l8I6n4acAi8)


---

## Objective

By the end of this session, you will:

* Design a real-world event-driven workflow.
* Trigger **Lambda** functions automatically on **S3 Uploads**.
* Send notifications via **Amazon SNS** upon successful processing.
* Implement error handling for failed events.

---

## Tools Used

* **Amazon S3** (Storage & Event Source)
* **AWS Lambda** (Compute)
* **Amazon SNS** (Notifications)
* **IAM Roles** (Security)

---

## Key Concepts

### 1. Event-Driven Architecture
The core idea is **decoupling**. The S3 bucket doesn't "know" about the Lambda function; it just emits an event. The Lambda function doesn't know about the user who uploaded the file; it just processes the data.

### 2. The Workflow
1.  **Ingest**: User uploads an invoice PDF to `input-bucket`.
2.  **Trigger**: S3 detects `ObjectCreated:Put` and invokes Lambda.
3.  **Process**: Lambda reads the file metadata (or content).
4.  **Notify**: Lambda publishes a message to an SNS Topic ("File received!").

### 3. IAM Permissions
Your Lambda role needs specific permissions:
*   `s3:GetObject` (To read the file)
*   `sns:Publish` (To send the email)
*   `logs:CreateLogGroup` (For CloudWatch)

---

## Key Concepts Applied

| Concept | Application |
| :--- | :--- |
| **S3 Notifications** | Configuring the bucket to send events to Lambda. |
| **Boto3 SDK** | Using Python to interact with AWS services (S3, SNS) inside the code. |
| **Environment Variables** | storing the SNS Topic ARN in Lambda configuration, not hard-coded in code. |

---

## Bonus (Extra Learning)

*   Try adding **DynamoDB** to log metadata of every processed file.
*   Implement a **Dead Letter Queue (DLQ)** for failed Lambda invocations.

---

## Congratulations!

You’ve built a fully automated cloud pipeline! This pattern (S3 -> Lambda -> SNS/DB) is one of the most common serverless patterns used in the industry.

---

## Try These Next

*   Modify the script to specific **resize an image** using the `Pillow` library in a Lambda Layer.
*   Secure your S3 bucket so only specific users can upload files.
