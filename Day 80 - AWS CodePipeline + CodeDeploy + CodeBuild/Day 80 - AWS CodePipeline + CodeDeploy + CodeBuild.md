# Day 80 - AWS CodePipeline + CodeDeploy + CodeBuild

Welcome to **Day 80** of the DevOps 90-Day Challenge!
We have used Jenkins and GitHub Actions. Now we use the **AWS Native** stack. If you work in an all-AWS shop, this is mandatory knowledge.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the AWS CI/CD suite.
* creating a `buildspec.yml` for **CodeBuild**.
* Creating an `appspec.yml` for **CodeDeploy**.
* Orchestrating the flow with **CodePipeline**.
* Deploying to EC2 (Blue/Green) and Lambda.

---

## Tools Used

* **AWS CodeCommit** (Git - optional)
* **AWS CodeBuild** (CI - compiles code)
* **AWS CodeDeploy** (CD - updates servers)
* **AWS CodePipeline** (Coordinator)

---

## Key Concepts

### 1. The Files
*   `buildspec.yml`: Instructions for CodeBuild. "Install nodejs, run npm test, run docker build".
*   `appspec.yml`: Instructions for CodeDeploy. "Stop server, copy files to /var/www, start server".

### 2. Deployment Strategies with CodeDeploy
*   **In-Place**: Stop app on Instance A, update it, start it. (Downtime).
*   **In-Place (Rolling)**: Update 1 server at a time.
*   **Blue/Green**: Spin up new Autoscaling Group (Green), deploy to it, switch Load Balancer traffic. (Zero Downtime, safer).

### 3. Pipeline Integration
CodePipeline listens to S3 or GitHub. When a change happens, it triggers Build -> Test -> Deploy Staging -> Approval -> Deploy Prod.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Artifacts** | passing the `myapp.zip` from Build stage to Deploy stage via S3 artifact store. |
| **Lambda Deploy** | Using CodeDeploy to shift traffic 10% every minute (Linear) to a new Lambda version. |
| **S3 Static Website** | Using CodePipeline to deploy a React app to an S3 bucket. |

---

## Bonus (Extra Learning)

*   Trigger a Lambda function inside CodePipeline to run a sanity check.
*   Use **AWS CodeStar** to set up a project in 5 minutes.

---

## Congratulations!

You are now certified in the "AWS Way" of doing DevOps.

---

## Try These Next

*   Migrate a Jenkins pipeline to CodePipeline.
*   Set up a manual approval step that sends an SMS to the manager.
