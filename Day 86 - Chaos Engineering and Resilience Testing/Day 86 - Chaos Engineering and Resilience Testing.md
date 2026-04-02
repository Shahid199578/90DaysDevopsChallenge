# Day 86 - Chaos Engineering and Resilience Testing

Welcome to **Day 86** of the DevOps 90-Day Challenge!
Today we test the High Availability (HA) systems we built. We will adopt the Netflix "Chaos Monkey" methodology to break things on purpose, proving that our infrastructure auto-heals without human intervention.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the philosophy and necessity of **Chaos Engineering**.
* Install the **Chaos Mesh** platform on Kubernetes.
* Design a chaos experiment and implement a **PodChaos** attack.
* Observe and validate Kubernetes Auto-healing mechanisms during a failure.

---

## Tools Used

* **Chaos Mesh**
* **Kubernetes (ReplicaSets / Deployments)**
* **Helm**

---

## Key Concepts

### 1. Chaos Engineering
Chaos Engineering is the discipline of experimenting on a system to build confidence in its capability to withstand turbulent conditions in production. You don't wait for a disaster; you trigger small controlled disasters to verify auto-recovery logic.

### 2. Hypothesis-Driven Fault Injection
Always inject faults with a hypothesis. E.g., "If I kill one database node, the ReplicaSet will instantly spin up a new one without affecting user traffic". 

### 3. Chaos Mesh
An open-source cloud-native chaos engineering platform that orchestrates fault injection seamlessly into Kubernetes clusters. It can simulate Pod failures, Network latency, DNS errors, and even kernel-level faults.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Deployment Resilience** | Deploying an Nginx application with 3 replicas to guarantee failover capacity. |
| **PodChaos Event** | Injecting a CRD (Custom Resource Definition) that instructs Chaos Mesh to randomly kill a pod every 10 seconds. |
| **Self-Healing** | Watching the Kubernetes control plane instantly detect the dead pod and rapidly recreate a replacement to maintain the desired state. |

---

## Bonus (Extra Learning)

* Try injecting a `NetworkChaos` experiment to simulate 500ms network latency and ping your application to observe the delay.
* Research **AWS Fault Injection Simulator (FIS)** for a managed AWS-native chaos experience.

---

## Congratulations!

You've successfully run live Chaos experiments! You now possess an elite DevOps mentality: expecting and designing for constant failure.
