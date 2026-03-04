# Day 82 - Handling Multi-Environment Deployments

Welcome to **Day 82** of the DevOps 90-Day Challenge!
"It works on my machine" is not an excuse. "It works in Dev but fails in Prod" is a tragedy. Today we learn to manage **Dev, Staging, and Production**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Structure your Infrastructure as Code for multiple environments.
* Manage **Configuration Drift**.
* Implement **Promotion Strategies** (Dev -> Stage -> Prod).
* Handle **Environment Variables** securely.

---

## Tools Used

* **Terraform** (Workspaces)
* **Helm** (Values files)
* **GitHub Actions** (Environments)

---

## Key Concepts

### 1. Terraform Strategies
*   **Workspaces**: `terraform workspace new dev`. Same .tf files, different state files. Good for similar envs.
*   **Directory Layout**: `envs/dev`, `envs/prod`. Each folder has its own `main.tf` and state. Good for isolating permissions (Prod has stricter IAM).

### 2. Helm Values
*   `values.yaml`: Defaults.
*   `values-dev.yaml`: Overrides (`replicaCount: 1`).
*   `values-prod.yaml`: Overrides (`replicaCount: 10`, `resources: limits: cpu: 1`).

### 3. Promotion Pipeline
The artifact (Docker Image) should be built **ONCE**.
1.  Build Image `v1.2`.
2.  Deploy `v1.2` to Dev. Test.
3.  Deploy `v1.2` to Stage. Test.
4.  Deploy `v1.2` to Prod.
*Never rebuild the image for Prod. You might get different dependencies.*

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Parity** | Trying to keep Dev and Prod as similar as possible (using same OS, same DB engine) to avoid surprises. |
| **Gating** | Adding a "Manual Approval" button in the pipeline before deploying to Prod. |
| **ConfigMaps** | Injecting `DB_HOST` via ConfigMap, so the code remains agnostic. |

---

## Bonus (Extra Learning)

*   Use **Terraform Cloud** to manage state locking and remote runs.
*   Implement **Ephemeral Environments** (spin up a temporary env for every Pull Request).

---

## Congratulations!

You have mastered the release lifecycle. This ensures stability and reliability.

---

## Try These Next

*   Create a "Hotfix" pipeline branch strategy.
*   Automate the cleanup of old environments.
