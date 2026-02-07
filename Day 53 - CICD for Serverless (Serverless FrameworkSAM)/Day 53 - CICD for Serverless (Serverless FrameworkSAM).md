# Day 53 - CICD for Serverless (Serverless Framework/SAM)

Welcome to **Day 53** of the DevOps 90-Day Challenge!
Today, we stop clicking in the console and start using **Infrastructure as Code (IaC)** for Serverless. We’ll explore the **Serverless Framework** and **AWS SAM**.

[![](https://img.youtube.com/vi/aoI50nl4MyM/0.jpg)](https://www.youtube.com/watch?v=aoI50nl4MyM)

[Watch the video](https://www.youtube.com/watch?v=aoI50nl4MyM)

---

## Objective

By the end of this session, you will:

* Install and configure the **Serverless Framework**.
* Define your Lambda functions and events in a `serverless.yml` file.
* Deploy your entire serverless application with a single command (`serverless deploy`).

---

## Tools Used

* **Serverless Framework** (CLI)
* **Node.js / NPM** (to install the framework)
* **AWS CLI** (for credentials)
* **AWS CloudFormation** (used under the hood)

---

## Key Concepts

### 1. Why use a Framework?

* **Version Control**: Your infrastructure is code (YAML).
* **Automation**: Deploying 10 functions is as easy as deploying 1.
* **Best Practices**: Frameworks handle IAM roles and packaging for you.

### 2. `serverless.yml` Structure

```yaml
service: my-service

provider:
  name: aws
  runtime: python3.9

functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: /hello
          method: get
```

### 3. Deployment Commands

```bash
# Deploy to AWS
serverless deploy

# Remove everything (Cleanup)
serverless remove
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **IaC** | Using YAML to define functions and APIs. |
| **CloudFormation** | Serverless Framework translates YAML to CF Stacks. |
| **Packaging** | Zipping code and dependencies automatically. |

---

## Bonus (Extra Learning)

* Try **AWS SAM** (Serverless Application Model), which is AWS's native competitor to Serverless Framework.
* Deploy a function with an **external python library** (e.g., `requests`) using a plugin.

---

## Congratulations!

You’ve successfully deployed a Serverless App using **IaC**!
No more manual clicks in the console. You are now a Serverless Professional.

---

## Try These Next

* Set up a **GitHub Action** that runs `serverless deploy` on push.
* managing **Environment Variables** in `serverless.yml`.
