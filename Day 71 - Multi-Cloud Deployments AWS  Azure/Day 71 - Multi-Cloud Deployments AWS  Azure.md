# Day 71 - Multi-Cloud Deployments (AWS + Azure)

Welcome to **Day 71** of the DevOps 90-Day Challenge!
Today, we step outside the AWS walled garden. **Multi-Cloud** is a reality for many enterprises. We will explore how to manage resources across **AWS** and **Microsoft Azure**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the drivers for Multi-Cloud (Compliance, Feature Selection, reliability).
* Connect AWS and Azure networks (VPN/Direct Connect).
* Use **Terraform** to provision resources in both clouds simultaneously.
* Compare AWS services to their Azure equivalents.

---

## Tools Used

* **Terraform**
* **AWS Console**
* **Azure Portal**

---

## Key Concepts

### 1. Service Mapping
| AWS | Azure |
| :--- | :--- |
| EC2 | Virtual Machine |
| VPC | VNet |
| S3 | Blob Storage |
| Lambda | Azure Functions |
| IAM Role | Managed Identity |

### 2. Terraform for Multi-Cloud
Terraform is the king of multi-cloud. You can define multiple `providers` in one file.

```hcl
provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  features {}
}

resource "aws_s3_bucket" "my_bucket" { ... }
resource "azurerm_storage_account" "my_storage" { ... }
```

### 3. Challenges
*   **Latency**: connecting app in AWS to DB in Azure adds latency.
*   **Data Egress Costs**: You pay to move data *out* of AWS to Azure.
*   **Complexity**: Need to learn two IAM models, two networking stacks.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Unified IaC** | Using one `main.tf` to spin up a VM in Azure and an S3 bucket in AWS. |
| **Site-to-Site VPN** | Conceptually linking the VPC and VNet for private communication. |
| **Identity** | Using Azure AD (Entra ID) to sign in to AWS Console (SSO). |

---

## Bonus (Extra Learning)

*   Create a free Azure account and spin up a VM using Terraform.
*   Explore **Google Cloud Platform (GCP)** services like BigQuery.

---

## Congratulations!

You are no longer just an "AWS Engineer"; you are a "Cloud Engineer". The skills to adapt to multiple platforms make you versatile and valuable.

---

## Try These Next

*   Use **Terraform Workspaces** to manage separate state files for AWS and Azure.
*   Deploy a Docker container to **Azure Container Instances (ACI)**.
