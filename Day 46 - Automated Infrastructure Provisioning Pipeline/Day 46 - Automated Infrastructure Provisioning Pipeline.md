# Day 46 - Automated Infrastructure Provisioning Pipeline

Welcome to **Day 46** of the DevOps 90-Day Challenge!
Today, we’ll bring together everything from Terraform and CloudFormation to build a **fully automated infrastructure provisioning pipeline** using CI/CD principles.

[![](https://img.youtube.com/vi/uOH__mqGNh0/0.jpg)](https://www.youtube.com/watch?v=uOH__mqGNh0)

[Watch the video](https://www.youtube.com/watch?v=uOH__mqGNh0)
---

##  Objective

By the end of this session, you will:

* Automate **infrastructure provisioning** using CI/CD.
* Integrate **Terraform and CloudFormation** with Jenkins or GitHub Actions.
* Achieve **repeatable, version-controlled infrastructure deployments**.

---

##  Tools Used

* **Jenkins or GitHub Actions**
* **Terraform CLI**
* **AWS CloudFormation**
* **AWS CLI & Account**
* **GitHub Repo** (for infrastructure code)

---

## Key Concepts

### 1. CI/CD for Infrastructure

* Treat **infrastructure code** like application code.
* Pipeline stages:

  1. **Checkout** code from GitHub
  2. **Lint / Validate** templates or Terraform files
  3. **Plan / Preview** changes
  4. **Apply / Deploy** after approval
  5. **Post-actions** (notify, logs, destroy in dev)

---

### 2. Sample Jenkins Pipeline (Terraform + CloudFormation)

```groovy
pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
    }

    stages {
        stage('Checkout') {
            steps { git branch: 'main', url: 'https://github.com/username/iac-pipeline.git' }
        }

        stage('Terraform Init & Plan') {
            steps {
                dir('terraform') {
                    sh 'terraform init'
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                dir('terraform') {
                    input message: 'Approve Terraform Apply?'
                    sh 'terraform apply tfplan'
                }
            }
        }

        stage('CloudFormation Deploy') {
            steps {
                dir('cloudformation') {
                    sh 'aws cloudformation deploy --stack-name cf-demo --template-file reusable-ec2.yaml --capabilities CAPABILITY_NAMED_IAM'
                }
            }
        }
    }

    post {
        always { echo 'Pipeline Completed' }
    }
}
```

---

### 3. GitHub Actions Alternative

```yaml
name: IaC Deployment
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
      - name: Terraform Init
        run: terraform init
      - name: Terraform Plan
        run: terraform plan -out=tfplan
      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
      - name: Deploy CloudFormation
        run: |
          aws cloudformation deploy \
          --stack-name cf-demo \
          --template-file cloudformation/reusable-ec2.yaml \
          --capabilities CAPABILITY_NAMED_IAM
```

---

### 4. Verification

* Terraform resources created → EC2, S3, IAM
* CloudFormation stack deployed → EC2 instance outputs available
* Pipeline logs → confirm successful execution

---

## Key Concepts Applied

| Concept                   | Example Used                                |
| ------------------------- | ------------------------------------------- |
| CI/CD Pipeline            | Jenkins or GitHub Actions                   |
| Terraform Automation      | init, plan, apply stages                    |
| CloudFormation Deployment | deploy stacks via CLI or pipeline           |
| Approval & Notifications  | input steps or GitHub Actions notifications |
| Repeatable Deployment     | Infrastructure as Code principle            |

---

## Bonus (Extra Learning)

* Add **multi-environment support** (dev, staging, prod)
* Enable **automatic rollback** on failure
* Integrate **Slack or Email notifications**

---

## Congratulations!

You’ve successfully built a **fully automated infrastructure provisioning pipeline**!
This approach ensures your cloud infrastructure is **version-controlled, repeatable, and production-ready**.

---

## Try These Next

* Implement **destroy pipelines** for dev environments
* Use **Terraform modules + CloudFormation nested stacks** together
* Extend pipeline for **multi-cloud deployments**


