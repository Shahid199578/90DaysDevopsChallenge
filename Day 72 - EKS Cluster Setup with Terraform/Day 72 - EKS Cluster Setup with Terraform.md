# Day 72 - EKS Cluster Setup with Terraform

Welcome to **Day 72** of the DevOps 90-Day Challenge!
Today starts our deep dive into **Kubernetes on AWS (EKS)**. We won't be clicking buttons. We are DevOps engineers; we use **Terraform** to build our production-grade cluster.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the architecture of EKS (Control Plane vs Worker Nodes).
* Write Terraform code to provision a VPC for EKS.
* Provision the **EKS Control Plane**.
* Provision **Managed Node Groups** (Worker Nodes).
* Update `kubeconfig` to connect to the new cluster.

---

## Tools Used

* **Terraform**
* **AWS EKS**
* **kubectl**
* **AWS CLI**

---

## Key Concepts

### 1. EKS Architecture
*   **Control Plane**: Managed by AWS. High availability across 3 AZs. You pay ~$72/month.
*   **Data Plane (Nodes)**: EC2 instances that run your pods. Managed by you (or Fargate).

### 2. Terraform EKS Module
We will use the official community module `terraform-aws-modules/eks/aws`. It simplifies hundreds of lines of resources (IAM roles, Security Groups, Auto Scaling) into a readable block.

```hcl
module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  cluster_name    = "my-cluster"
  cluster_version = "1.27"
  
  eks_managed_node_groups = {
    general = {
      min_size     = 1
      max_size     = 3
      instance_types = ["t3.medium"]
    }
  }
}
```

### 3. Connecting
After `terraform apply`, you need to configure `kubectl`:
```bash
aws eks update-kubeconfig --region ap-south-1 --name my-cluster
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **VPC CNI** | The networking plugin that gives Pods real VPC IP addresses. |
| **IAM OIDC Provider** | Enabling IRSA (IAM Roles for Service Accounts) so pods can talk to AWS services. |
| **Node Groups** | Creating a scaling group of Worker Nodes managed by EKS. |

---

## Bonus (Extra Learning)

*   Add a **Fargate Profile** to run serverless pods.
*   Install the **EBS CSI Driver** addon using Terraform to allow persistent volumes.

---

## Congratulations!

You have a running kubernetes cluster! Provisioning EKS is notoriously complex, but Terraform makes it manageable and repeatable.

---

## Try These Next

*   Deploy a **Sample App** (Nginx) to your new cluster.
*   Destroy the cluster (`terraform destroy`) to avoid costs!
