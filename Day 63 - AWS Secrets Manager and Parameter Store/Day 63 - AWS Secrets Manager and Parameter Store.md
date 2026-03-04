# Day 63 - AWS Secrets Manager and Parameter Store

Welcome to **Day 63** of the DevOps 90-Day Challenge!
Today, we solve the eternal problem: **Where do I put my database password?** Hardcoding it in git is a security sin. We will learn to use **AWS Secrets Manager** and **Parameter Store**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the difference between **Secrets Manager** and **Parameter Store**.
* Store and retrieve a database password securely.
* Automate **Secret Rotation** (changing the password every 30 days automatically).
* Integrate secrets into your application code (without hardcoding!).

---

## Tools Used

* **AWS Secrets Manager**
* **AWS Systems Manager Parameter Store**
* **AWS KMS** (Key Management Service)
* **AWS Lambda** (for rotation)

---

## Key Concepts

### 1. Parameter Store (SSM)
*   **Cost**: Free (Standard tier).
*   **Use Case**: Configuration data (API URLs, License Keys) and simple secrets (Passwords).
*   **Features**: Versioning, Hierarchy (`/prod/db/password`), and Encryption via KMS.

### 2. Secrets Manager
*   **Cost**: Paid ($0.40 per secret/month).
*   **Use Case**: Highly sensitive credentials (DB passwords, API keys) that need **rotation**.
*   **Features**: Built-in rotation for RDS/Redshift/DocumentDB.

### 3. KMS Encryption
Both services use **KMS** to encrypt data at rest. You control who can decrypt the secret by managing KMS Key policies.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **SecureString** | Storing a password in Parameter Store so it's encrypted in the console. |
| **Dynamic Reference** | Using `{{resolve:secretsmanager:MySecret}}` in CloudFormation to inject secrets without revealing them. |
| **Rotation** | Configuring a Lambda function to update the DB password every 30 days. |

---

## Bonus (Extra Learning)

*   Create a **Hierarchy** in Parameter Store: `/dev/app/db_url` vs `/prod/app/db_url`.
*   Use the **AWS CLI** to retrieve a secret: `aws ssm get-parameter --name /my/secret --with-decryption`.

---

## Congratulations!

You’ve eliminated hardcoded credentials from your code! This is a massive security win and a requirement for SOC2/ISO compliance.

---

## Try These Next

*   Update your **Elastic Beanstalk** or **ECS** task definition to pull environment variables from Secrets Manager.
*   Audit who accessed a secret using **CloudTrail**.
