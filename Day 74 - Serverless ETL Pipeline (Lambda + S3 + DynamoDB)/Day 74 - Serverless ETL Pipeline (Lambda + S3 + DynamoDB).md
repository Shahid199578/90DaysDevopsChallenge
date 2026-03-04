# Day 74 - Serverless ETL Pipeline (Lambda + S3 + DynamoDB)

Welcome to **Day 74** of the DevOps 90-Day Challenge!
Today we build a data processing pipeline. In the real world, you often need to transform data (Extract, Transform, Load) without managing servers. We will use **AWS Lambda**, **S3**, and **DynamoDB**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand **ETL** architecture in a serverless context.
* Trigger a **Lambda** function when a CSV file is uploaded to **S3**.
* Parse the CSV data using Python (Pandas or built-in csv).
* Insert the processed data into a **DynamoDB** table.

---

## Tools Used

* **AWS S3** (Source)
* **AWS Lambda** (Compute/Transform)
* **Amazon DynamoDB** (Destination)
* **Python**

---

## Key Concepts

### 1. The Trigger
S3 Event Notifications. When a `PutObject` event happens in the `input/` folder, S3 sends the event JSON to Lambda.
```json
{
  "Records": [
    {
      "s3": {
        "bucket": { "name": "my-bucket" },
        "object": { "key": "data.csv" }
      }
    }
  ]
}
```

### 2. DynamoDB PutItem
DynamoDB is a NoSQL database. It's perfect for high-speed writes from Lambda.
We use `boto3` to write items.
`table.put_item(Item={'id': '123', 'value': 'test'})`

### 3. Error Handling
What if the CSV is malformed?
*   Use a **Dead Letter Queue (DLQ)** (SQS) to capture failed events.
*   Check CloudWatch Logs for stack traces.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Batch Processing** | Processing rows one by one vs batch_writer for DynamoDB efficiency. |
| **IAM Roles** | Granting the Lambda function `s3:GetObject` and `dynamodb:PutItem`. |
| **Infrastructure as Code** | Defining this whole stack in SAM or Terraform (Bonus). |

---

## Bonus (Extra Learning)

*   Add a transformation step (e.g., convert Fahrenheit to Celsius) before saving to DB.
*   Use **AWS Glue** for more complex ETL jobs.

---

## Congratulations!

You have built a Serverless Data Pipeline! This is a very common interview task for Data Engineers and DevOps Engineers.

---

## Try These Next

*   Visualize the data in DynamoDB using a simple frontend.
*   Trigger an SNS email when the ETL job finishes.
