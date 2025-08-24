# Day 42 - Advanced Terraform Concepts (Modules, Remote Backends)

Welcome to **Day 42** of the DevOps 90-Day Challenge!
Yesterday, you learned Terraform **state management and workspaces**.
Today, we’ll dive into **advanced concepts**: **modules** for reusable code and **remote backends** for collaboration.

[![](https://img.youtube.com/vi/wggQpvn1Wxk/0.jpg)](https://www.youtube.com/watch?v=wggQpvn1Wxk)

[Watch the video](https://www.youtube.com/watch?v=wggQpvn1Wxk)
---

## Objective

By the end of this session, you will:

* Understand **Terraform modules** and create reusable infrastructure code.
* Use **remote backends** to store state centrally.
* Organize Terraform projects for **scalability and maintainability**.

---

## Tools Used

* **Terraform CLI**
* **AWS S3 + DynamoDB** (remote state backend)
* **VS Code**

---

## Key Concepts

### 1. Terraform Modules

* Modules are **reusable Terraform configurations**.
* Can be **local** or **remote** (Terraform Registry, GitHub).
* Helps maintain **DRY (Don't Repeat Yourself)** principle.

**Example: Creating a Module for EC2**

```bash
terraform-demo/
 ├── modules/
 │    └── ec2/
 │         ├── main.tf
 │         ├── variables.tf
 │         └── outputs.tf
 └── main.tf
```

**`modules/ec2/main.tf`**

```hcl
resource "aws_instance" "this" {
  ami           = var.ami
  instance_type = var.instance_type
  tags = {
    Name = var.name
  }
}
```

**`modules/ec2/variables.tf`**

```hcl
variable "ami" {}
variable "instance_type" {}
variable "name" {}
```

**`modules/ec2/outputs.tf`**

```hcl
output "instance_id" {
  value = aws_instance.this.id
}
```

**Use Module in Root `main.tf`**

```hcl
module "web_server" {
  source        = "./modules/ec2"
  ami           = "ami-0abcdef1234567890"
  instance_type = "t2.micro"
  name          = "WebServer"
}
```

---

### 2. Remote Backend

* Use S3 + DynamoDB for **centralized state management and locking**.

**Example Remote Backend**

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-demo"
    key            = "project/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-lock"
    encrypt        = true
  }
}
```

* Allows **teams to collaborate safely** without overwriting state.

---

### 3. Apply Terraform

```bash
terraform init      # initialize backend
terraform plan
terraform apply
```

* Terraform fetches module code automatically
* Deploys infrastructure according to module definitions

---

### 4. Verify

* EC2 instance created from **module**
* State stored in **S3 bucket**
* DynamoDB ensures **locking during concurrent changes**

---

## Key Concepts Applied

| Concept          | Example Used                             |
| ---------------- | ---------------------------------------- |
| Modules          | `modules/ec2` reusable configuration     |
| Inputs & Outputs | Pass variables to modules, get outputs   |
| Remote Backend   | S3 + DynamoDB for shared state           |
| Scalability      | Use modules for multi-environment setups |

---

## Bonus (Extra Learning)

* Use **Terraform Registry modules** (e.g., `terraform-aws-modules/ec2-instance/aws`)
* Combine **multiple modules** to deploy full infrastructure stack
* Automate backend initialization in CI/CD pipelines

---

## Congratulations!

You’ve now mastered **Terraform modules** and **remote backends**!
This makes your infrastructure **reusable, maintainable, and collaborative**.

---

## Try These Next

* Create a module for **S3 bucket**
* Combine EC2 + S3 modules in a single root module
* Test **remote state collaboration** with multiple users

