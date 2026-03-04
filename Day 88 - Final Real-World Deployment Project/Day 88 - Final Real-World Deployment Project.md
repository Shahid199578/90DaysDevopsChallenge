# Day 88 - Final Real-World Deployment Project

Welcome to **Day 88** of the DevOps 90-Day Challenge!
We are approaching the finish line. Today we deploy a complex, microservices-based application that mimics a real-world scenario (e.g., An E-Commerce Store with Payments, User, and Catalog services).

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Clone the **Microservices Demo** (like Google's Hipster Shop or Sock Shop).
* Dockerize multiple services (Polyglot: Go, Java, NodeJS).
* Deploy to **Kubernetes** using Helm.
* Expose via **Ingress Controller** with HTTPS (Cert-Manager).

---

## Tools Used

* **Kubernetes (EKS/Minikube)**
* **Helm**
* **Cert-Manager** (Let's Encrypt)
* **Ingress Nginx**

---

## Key Concepts

### 1. The Architecture
*   **Frontend**: React/NodeJS.
*   **Backend**: 5 different services talking via gRPC or REST.
*   **Database**: Redis (Cache) and MongoDB (Product Data).
*   **Message Queue**: RabbitMQ (Async processing).

### 2. Service Discovery
How does Frontend find the Product Service? K8s DNS: `http://product-service.default.svc.cluster.local`.

### 3. Persistence
Ensuring MongoDB uses a Persistent Volume Claim (PVC) so data survives pod restarts.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Namespace Isolation** | Deploying into `shop-prod` namespace. |
| **Secrets** | Creating K8s Secrets for the payment gateway API keys. |
| **Resilience** | Configuring Liveness and Readiness probes so K8s restarts stuck services. |

---

## Bonus (Extra Learning)

*   Load test the application with **K6** or **JMeter**.
*   Observe the dependency graph using **Weave Scope** or **Kiali**.

---

## Congratulations!

You have deployed a system complex enough to run a business. This is the culmination of your technical skills.

---

## Try These Next

*   Implement a backup strategy for the MongoDB.
*   Scale the frontend to 10 replicas and watch the load balancer distribute traffic.
