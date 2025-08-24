# Day 41 - Terraform State Management and Workspaces

Welcome to **Day 41** of the DevOps 90-Day Challenge!
Yesterday, you provisioned AWS resources using Terraform.
Today, we’ll focus on **state management** and **workspaces**, crucial for collaboration and multi-environment setups.

[![](https://img.youtube.com/vi/Vo2K0Wqxb6E/0.jpg)](https://www.youtube.com/watch?v=Vo2K0Wqxb6E)
[Watch the video](https://www.youtube.com/watch?v=Vo2K0Wqxb6E)
---

## Objective

By the end of this session, you will:

* Understand **Terraform state files** and their purpose.
* Learn **local vs remote state**.
* Create and use **Terraform workspaces** for multiple environments.

---

## Tools Used

* **Terraform CLI**
* **AWS S3 & DynamoDB** (for remote state locking)
* **VS Code**

---

## Key Concepts

### 1. Terraform State

* Terraform keeps track of your infrastructure using a **state file** (`terraform.tfstate`).
* Contains:

  * Resource IDs
  * Metadata
  * Dependency graph
* **Important:** Never manually edit this file.

---

### 2. Local vs Remote State

* **Local State**: Stored on your machine (`terraform.tfstate`)
* **Remote State**: Stored in a remote backend (S3, GCS, Azure Blob)
* **Benefits of Remote State:**

  * Collaboration across team members
  * Locking to prevent concurrent changes

**Example Remote Backend (`main.tf`):**

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

---

### 3. Terraform Workspaces

* Workspaces allow **multiple states for same configuration**.
* Useful for environments like **dev, staging, prod**.

**Create and Switch Workspace**

```bash
terraform workspace list          # list existing workspaces
terraform workspace new dev       # create new workspace
terraform workspace select dev    # switch to workspace
```

* Each workspace maintains a **separate state file**.

---

### 4. Apply Terraform in Different Workspaces

```bash
terraform init
terraform workspace select dev
terraform plan
terraform apply
```

* Repeat for `staging` or `prod` workspace

---

### 5. Verify

* Remote state stored in **S3**
* DynamoDB table provides **locking mechanism**
* Separate environments isolated with **workspaces**

---

## Key Concepts Applied

| Concept               | Example Used                          |
| --------------------- | ------------------------------------- |
| State File            | `terraform.tfstate` (local or remote) |
| Remote Backend        | S3 + DynamoDB for locking             |
| Workspaces            | dev, staging, prod                    |
| Environment Isolation | Multiple states for same config       |

---

## Bonus (Extra Learning)

* Enable **state versioning** in S3
* Automate workspace creation in CI/CD pipelines
* Use **Terraform Cloud** for managed remote state

---

## Congratulations!

You now understand **Terraform state management** and **workspaces**, essential for safe multi-environment infrastructure deployments

---

## Try These Next

* Create **staging** workspace and deploy same infrastructure
* Test **concurrent changes** and observe locking mechanism
* Use remote backend with **encryption enabled**

