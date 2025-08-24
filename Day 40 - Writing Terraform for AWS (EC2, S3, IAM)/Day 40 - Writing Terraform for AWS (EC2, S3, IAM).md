# Day 40 - Writing Terraform for AWS (EC2, S3, IAM)
Welcome to **Day 40** of the DevOps 90-Day Challenge!
Yesterday, you learned the basics of Terraform.
Today, you’ll create **AWS infrastructure** including **EC2 instances, S3 buckets, and IAM users** using Terraform.

[![](https://img.youtube.com/vi/EUOXrt-Dtjk/0.jpg)](https://www.youtube.com/watch?v=EUOXrt-Dtjk)
[Watch the video](https://www.youtube.com/watch?v=EUOXrt-Dtjk)
---

## Objective

By the end of this session, you will:

* Provision **EC2 instances**.
* Create **S3 buckets**.
* Manage **IAM users and policies**.
* Learn to structure Terraform files for AWS projects.

---

## Tools Used

* **Terraform CLI**
* **AWS Account** (with IAM permissions)
* **VS Code or any text editor**

---

## Directory Structure

```bash
aws-terraform-demo/
 ├── main.tf
 ├── variables.tf
 ├── outputs.tf
 └── iam.tf
```

---

## Step-by-Step Guide

### 1. Provider Setup

**`main.tf`**

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

---

### 2. EC2 Instance

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcdef1234567890" # Replace with valid AMI
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformDemoEC2"
  }
}
```

---

### 3. S3 Bucket

```hcl
resource "aws_s3_bucket" "demo_bucket" {
  bucket = "terraform-demo-bucket-12345"
  acl    = "private"

  tags = {
    Name = "TerraformDemoBucket"
  }
}
```

---

### 4. IAM User

**`iam.tf`**

```hcl
resource "aws_iam_user" "demo_user" {
  name = "terraform-demo-user"
}

resource "aws_iam_access_key" "demo_key" {
  user = aws_iam_user.demo_user.name
}

output "access_key_id" {
  value = aws_iam_access_key.demo_key.id
}

output "secret_access_key" {
  value = aws_iam_access_key.demo_key.secret
}
```

---

### 5. Variables (Optional)

**`variables.tf`**

```hcl
variable "region" {
  description = "AWS Region"
  default     = "ap-south-1"
}

variable "instance_type" {
  description = "EC2 instance type"
  default     = "t2.micro"
}
```

---

### 6. Apply Terraform

```bash
terraform init
terraform plan
terraform apply
```

* Confirm with **yes** when prompted

---

### 7. Verify

* EC2 instance is running → AWS Console → EC2
* S3 bucket created → AWS Console → S3
* IAM user and access keys → AWS Console → IAM

---

## Key Concepts Applied

| Concept   | Example Used                          |
| --------- | ------------------------------------- |
| EC2       | `aws_instance`                        |
| S3 Bucket | `aws_s3_bucket`                       |
| IAM User  | `aws_iam_user` & `aws_iam_access_key` |
| Variables | `variables.tf`                        |
| Output    | `outputs.tf`                          |

---

## Bonus (Extra Learning)

* Attach **IAM Policy** to the user: `AdministratorAccess`
* Enable **versioning** for S3 bucket
* Use **Terraform modules** for reusable AWS resources

---

## Congratulations!

You’ve successfully provisioned **EC2, S3, and IAM** resources using Terraform
This is the foundation for **automated cloud infrastructure management**.

---

## Try These Next

* Create multiple EC2 instances using `count` or `for_each`.
* Enable **public access block** for S3 bucket.
* Store Terraform state in **remote backend** (S3 + DynamoDB).

