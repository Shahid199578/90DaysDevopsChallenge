# Day 43 - Terraform + Jenkins CI/CD Integration


Welcome to **Day 43** of the DevOps 90-Day Challenge!
Yesterday, you learned **advanced Terraform concepts**.
Today, we’ll integrate Terraform with **Jenkins** to automate infrastructure provisioning using **CI/CD pipelines**.

[![](https://img.youtube.com/vi/738afAnLrO0/0.jpg)](https://www.youtube.com/watch?v=738afAnLrO0)
[Watch the video](https://www.youtube.com/watch?v=738afAnLrO0)
---

## Objective

By the end of this session, you will:

* Understand how to **automate Terraform** using Jenkins pipelines.
* Learn to run **plan, apply, and destroy** Terraform tasks via Jenkins.
* Implement **safe, repeatable infrastructure deployment**.

---

## Tools Used

* **Terraform CLI**
* **Jenkins** (installed on EC2 or local)
* **AWS Account**
* **GitHub Repo** (for Terraform code)

---

## Step-by-Step Guide

### 1. Jenkins Pipeline Setup

* Create a **Jenkins Pipeline Job**
* Connect to your **GitHub repository** containing Terraform code

---

### 2. Sample Declarative Jenkinsfile

```groovy
pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/username/terraform-demo.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: 'Approve Apply?'
                sh 'terraform apply tfplan'
            }
        }
    }

    post {
        always {
            echo 'Pipeline Completed'
        }
    }
}
```

---

### 3. Configure Jenkins Credentials

* Go to **Jenkins → Credentials → Global**
* Add AWS keys as **“aws-access-key”** and **“aws-secret-key”**

---

### 4. Run the Pipeline

* Trigger **Build Now**
* Jenkins will:

  1. Checkout code
  2. Initialize Terraform
  3. Generate plan
  4. Wait for manual approval
  5. Apply changes

---

### 5. Verification

* Check **AWS Console** → resources created (EC2, S3, IAM)
* Review **Jenkins console logs** for errors
* Terraform state saved remotely (if configured)

---

## Key Concepts Applied

| Concept              | Example Used                          |
| -------------------- | ------------------------------------- |
| CI/CD Integration    | Jenkins Pipeline runs Terraform tasks |
| Terraform Automation | init, plan, apply stages              |
| Secrets Management   | Jenkins credentials for AWS           |
| Manual Approval      | `input` step before apply             |

---

## Bonus (Extra Learning)

* Add **destroy stage** to clean up infrastructure
* Integrate **Slack notifications** for pipeline success/failure
* Parameterize pipeline for **different environments**

---

## Congratulations!

You’ve successfully integrated **Terraform with Jenkins**!
Now your infrastructure can be deployed automatically, safely, and repeatably.

---

## Try These Next

* Add **staging and production pipelines**
* Use **multi-branch pipeline** to deploy feature-specific environments
* Automate remote state setup using **S3 backend**

