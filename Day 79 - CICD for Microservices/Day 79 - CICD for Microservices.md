# Day 79 - CI/CD for Microservices

Welcome to **Day 79** of the DevOps 90-Day Challenge!
Today, we’ll explore how to design and implement **CI/CD pipelines** specifically tailored for **Microservices Architecture**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com/watch?v=placeholder)

[Watch the video](https://www.youtube.com/watch?v=placeholder)

---

## Objective

By the end of this session, you will:

* Understand the difference between **Monorepo** and **Polyrepo** strategies.
* Learn how to detect changes in specific microservices ("Smart Builds").
* Create a Jenkinsfile that handles independent deployments for multiple services.
* Deploy microservices to Kubernetes without affecting other services.

---

## Tools Used

* **Jenkins** (CI/CD Orchestrator)
* **Docker** (Containerization)
* **Kubernetes** (Orchestration)
* **Git** (Version Control)
* **Groovy** (Jenkins Pipeline Scripting)

---

## Key Concepts

### 1. Monorepo vs. Polyrepo

* **Monorepo**: All microservices (Service A, Service B, API Gateway) live in a **single Git repository**.
    * **Pros**: Easy code sharing, atomic commits across services, simplified dependency management.
    * **Cons**: Large repo size, complex CI logic needed to avoid rebuilding everything on every commit.

* **Polyrepo**: Each microservice has its **own Git repository**.
    * **Pros**: Clear ownership, independent build pipelines, smaller repo size.
    * **Cons**: Difficult to manage shared code, complex cross-service changes.

### 2. "Smart" Change Detection

In a Monorepo, if you modify *Service A*, you shouldn't rebuild *Service B*. We use logic to detect which folder changed.

**Example Logic:**
`git diff --name-only HEAD HEAD~1` -> Check if output contains "service-a/".

### 3. Independent Deployments

Microservices must be deployable independently. A failure in *Service A's* pipeline should not block *Service B's* deployment.

---

## Lab Tasks

### 1. Structure Your Monorepo
Create a folder structure like this:
```
my-microservices-repo/
├── service-a/
│   ├── Dockerfile
│   └── app.py
├── service-b/
│   ├── Dockerfile
│   └── app.js
└── Jenkinsfile
```

### 2. Create a "Smart" Jenkinsfile
Use the `changeset` condition in Jenkins Declarative Pipeline to trigger stages only when relevant files change.

**Sample Jenkinsfile:**

```groovy
pipeline {
    agent any
    stages {
        stage('Build Service A') {
            when {
                changeset "service-a/**"
            }
            steps {
                echo "Building Service A..."
                sh 'cd service-a && docker build -t my-repo/service-a:latest .'
            }
        }
        stage('Build Service B') {
            when {
                changeset "service-b/**"
            }
            steps {
                echo "Building Service B..."
                sh 'cd service-b && docker build -t my-repo/service-b:latest .'
            }
        }
    }
}
```

### 3. Deploy to Kubernetes
Add a deploy stage that updates only the specific deployment for the changed service using `kubectl set image`.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Monorepo** | Managing Service A and B in one repo. |
| **Changeset** | Jenkins feature to detect modified files. |
| **Independent Deploy** | Building Service A doesn't touch Service B. |
| **Atomic Commits** | Making changes to both services in one PR. |

---

## Bonus (Extra Learning)

* Explore **Bazel** or **Nx** for advanced monorepo build tools.
* Learn about **Helm Library Charts** to share common K8s templates across microservices.

---

## Congratulations!

You’ve successfully implemented a **CI/CD strategy for Microservices**!
Managing pipelines for distributed systems is a critical skill in modern DevOps.

---

## Try These Next

* Implement **ArgoCD** to handle the deployment side (GitOps).
* Add a **Shared Library** in Jenkins to reuse pipeline code across multiple microservice repos (if using Polyrepo).
