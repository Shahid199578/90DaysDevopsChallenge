# Day 74 - Kubernetes Service Mesh with Istio

Welcome to **Day 74** of the DevOps 90-Day Challenge!
Today, we transition from basic Kubernetes networking into advanced microservices management using **Istio**, the industry standard Service Mesh platform.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the difference between the **Data Plane** and **Control Plane**.
* Install Istio using `istioctl`.
* Implement **Sidecar Injection** into application pods.
* Secure intra-cluster traffic seamlessly using **Mutual TLS (mTLS)**.

---

## Tools Used

* **Istio** (Service Mesh)
* **Envoy** (Sidecar Proxy)
* **Kubernetes (EKS)**

---

## Key Concepts

### 1. Service Mesh
A dedicated infrastructure layer that handles communication between microservices. It intercepts all traffic and handles load balancing, service-to-service authentication, and monitoring, completely transparently to the application.

### 2. Envoy Proxy Sidecars
Istio injects an Envoy proxy container into every pod you deploy. This proxy intercepts all incoming and outgoing HTTP/TCP traffic for that pod, encrypting it and enforcing rules before it ever reaches the application container.

### 3. Mutual TLS (mTLS)
mTLS ensures that traffic between services is encrypted. Not only does the client verify the server's certificate, but the server also verifies the client's certificate. Istio does this automatically without needing to configure SSL certificates in your app code.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Automatic Injection** | Labeling a namespace with `istio-injection=enabled` so K8s handles Envoy for us. |
| **Zero-Code Security** | Applying a `PeerAuthentication` policy to enforce STRICT mTLS across the cluster. |
| **Traffic Splitting (Theory)** | Using VirtualServices to send 90% of traffic to v1, and 10% to v2 (Canary release). |

---

## Bonus (Extra Learning)

* Configure a Gateway to expose an application to outside traffic using Istio instead of a standard Ingress.
* Try deploying Kiali to visually map and inspect your Service Mesh telemetry.

---

## Congratulations!

You have entered the realm of advanced Kubernetes networking! You can now secure and route complex microservices without touching developer code.
