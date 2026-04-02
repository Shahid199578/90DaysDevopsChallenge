# Day 77 - Kubernetes Autoscaling

Welcome to **Day 77** of the DevOps 90-Day Challenge!
Today, we focus on dynamic scaling. True cloud-native applications scale seamlessly with traffic without manual intervention. We will conquer both Pod-level scaling and Node-level scaling.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Deploy and understand the **Kubernetes Metrics Server**.
* Configure the **Horizontal Pod Autoscaler (HPA)** based on CPU utilization.
* Understand the paradigm shift introduced by **Karpenter** for Node scaling.
* Perform a live stress test to validate auto-scaling behavior.

---

## Tools Used

* **Horizontal Pod Autoscaler (HPA)**
* **Karpenter / Cluster Autoscaler**
* **Metrics Server**

---

## Key Concepts

### 1. HPA (Horizontal Pod Autoscaler)
HPA automatically updates a workload resource (like a Deployment) to match demand. If CPU utilization suddenly spikes above a defined threshold, HPA instructs the ReplicaSet to spawn additional pods to handle the load.

### 2. Karpenter vs Cluster Autoscaler
If HPA scaling exhausts your cluster’s available node memory/CPU, pods go into a `Pending` state. AWS Karpenter continuously observes these pending pods and provisions the optimal EC2 Instance types in seconds, far faster than traditional ASG-based Cluster Autoscalers.

### 3. Metrics Exposing
HPA cannot function natively. It relies entirely on the `metrics-server` which scrapes raw resource usage data from Kubelets on every node and exposes them via the Metrics API.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Resource Requests** | Defining CPU limits on your Deployment so K8s can calculate percentage-based utilization. |
| **Load Generation** | Running a BusyBox loop to slam the application with requests and trigger the HPA. |
| **Dynamic Provisioning** | Observing K8s scaling from 1 replica up to 10 replicas automatically depending on traffic spikes. |

---

## Bonus (Extra Learning)

* Research **VPA (Vertical Pod Autoscaler)** and note the differences between scaling *out* (HPA) vs scaling *up* (VPA).
* Learn about KEDA (Kubernetes Event-driven Autoscaling) for scaling based on SQS/RabbitMQ queues.

---

## Congratulations!

Your applications are now resilient to traffic storms! Operations won't be woken up at 3 AM because a server was overwhelmed.
