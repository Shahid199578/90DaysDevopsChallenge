# Day 73 - Jenkins Pipelines for Kubernetes

Welcome to **Day 73** of the DevOps 90-Day Challenge!
Today, we connect our two favorite tools: **Jenkins** and **Kubernetes**. We will build a pipeline that builds a Docker image and deploys it to our new EKS cluster.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Install the **Kubernetes Plugin** in Jenkins.
* Configure Jenkins to talk to your EKS Cluster (`kubeconfig`).
* Write a pipeline that runs `kubectl apply`.
* Implement the **Rolling Update** strategy via CI/CD.

---

## Tools Used

* **Jenkins**
* **Docker**
* **Kubernetes (EKS)**
* **kubectl**

---

## Key Concepts

### 1. The Workflow
1.  **Commit**: Developer pushes code to GitHub.
2.  **Build**: Jenkins checks out code, builds Docker image.
3.  **Push**: Jenkins pushes image to ECR/DockerHub.
4.  **Deploy**: Jenkins runs `kubectl set image` to update the deployment in EKS.

### 2. Authentication
Jenkins needs permission to talk to EKS.
*   **Service Account**: Create a ServiceAccount in K8s and generate a token.
*   **Kubeconfig**: Store the token as a Secret in Jenkins ("Secret Text").

### 3. Pipeline Syntax
```groovy
stage('Deploy to K8s') {
    steps {
        withKubeConfig([credentialsId: 'k8s-token', serverUrl: 'https://...']) {
            sh 'kubectl set image deployment/myapp myapp=myimage:v2'
        }
    }
}
```

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Credential Binding** | securely injecting the K8s token into the pipeline environment. |
| **Image Tagging** | Using the `BUILD_NUMBER` as the image tag (`v1.0.55`) for traceability. |
| **Validation** | Running `kubectl rollout status` to verify the deployment succeeded. |

---

## Bonus (Extra Learning)

*   Run Jenkins **Agents as Pods** inside the Kubernetes cluster (Dynamic Agents). This saves money as agents only exist when a job is running.
*   Use a **Helm** step in Jenkins to deploy a chart instead of raw manifests.

---

## Congratulations!

You have automated the "Last Mile" of deployment. Your code now goes from laptop to production cluster without human intervention.

---

## Try These Next

*   Implement a **Canary Deployment** pipeline (deploy to 10% of pods first).
*   Add a **manual approval** step before deploying to Production.
