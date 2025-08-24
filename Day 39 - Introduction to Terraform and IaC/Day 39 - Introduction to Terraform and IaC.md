# Day 39 - Introduction to Terraform and IaC
Welcome to **Day 39** of the DevOps 90-Day Challenge!
Today, we begin the **Infrastructure as Code (IaC)** section with **Terraform**, a powerful tool to manage cloud infrastructure declaratively.

[![](https://img.youtube.com/vi/MQSO0inK_-k/0.jpg)](https://www.youtube.com/watch?v=MQSO0inK_-k)
[Watch the video](https://www.youtube.com/watch?v=MQSO0inK_-k)
---

## Objective

By the end of this session, you will:

* Understand the concept of **IaC**.
* Learn what **Terraform** is and why it’s useful.
* Write your first **Terraform configuration**.

---

## Tools Used

* **Terraform CLI**
* **AWS Account** (for practical examples)
* **Text Editor** (VS Code, Vim, etc.)

---

## Key Concepts

### 1. Infrastructure as Code (IaC)

* IaC lets you **define infrastructure using code**.
* Benefits:

  * **Version Control** (track infrastructure changes).
  * **Consistency** (same config in dev, staging, prod).
  * **Automation** (deploy infrastructure automatically).

### 2. Terraform Overview

* **Open-source IaC tool** by HashiCorp.
* Works with multiple providers (AWS, Azure, GCP, Kubernetes).
* Core concepts:

  * **Provider**: Specifies which cloud platform (e.g., AWS).
  * **Resource**: Defines infrastructure components (EC2, S3).
  * **State**: Keeps track of deployed resources.

---

## Directory Structure

```bash
terraform-demo/
 ├── main.tf
 ├── variables.tf
 └── outputs.tf
```

---

## Step-by-Step Guide

### 1. Install Terraform

```bash
# Ubuntu
sudo apt update
sudo apt install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
sudo apt-add-repository "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update && sudo apt install terraform
terraform -v
```

---

### 2. Create a Provider

**`main.tf`**

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

---

### 3. Define a Resource (Example: EC2 Instance)

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcdef1234567890" # replace with valid AMI
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformDemo"
  }
}
```

---

### 4. Initialize and Apply Terraform

```bash
terraform init   # initialize Terraform
terraform plan   # preview changes
terraform apply  # create resources
```

* Type **yes** when prompted

---

### 5. Verify

* Check AWS console → EC2 → Instance running
* Terraform tracks state in `terraform.tfstate`

---

## Key Concepts Applied

| Concept      | Example Used                         |
| ------------ | ------------------------------------ |
| Provider     | AWS (`provider "aws"`)               |
| Resource     | EC2 instance (`aws_instance`)        |
| State        | `terraform.tfstate` file             |
| Plan & Apply | `terraform plan` & `terraform apply` |

---

## Bonus (Extra Learning)

* Add **outputs.tf** to get instance public IP:

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

* Use **variables.tf** for parameterized configurations.
* Destroy resources safely: `terraform destroy`

---

## Congratulations!

You’ve deployed your **first cloud resource using Terraform**!
This is the foundation for **automating entire cloud environments** using code.

---

## Try These Next

* Add **S3 bucket** using Terraform.
* Use **Terraform variables** to make code reusable.
* Track state using **remote backend** (S3 + DynamoDB).

