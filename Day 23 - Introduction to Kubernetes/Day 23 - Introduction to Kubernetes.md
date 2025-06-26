# Day 23 - Introduction to Kubernetes
Welcome to Day 23 of the 90 Days of DevOps Challenge! Today, we begin our journey into **Kubernetes** — the most widely used container orchestration platform.

---

## 🌟 What is Kubernetes?

**Kubernetes** (also known as **K8s**) is an open-source container orchestration platform that automates:

- Deployment
- Scaling
- Management
- Networking
- Availability

of containerized applications.

Originally developed by Google and now maintained by the **Cloud Native Computing Foundation (CNCF)**.

---

## 🧱 Why Kubernetes?

| Feature              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **High Availability** | Keeps your applications running even if a node fails.                      |
| **Auto-Scaling**      | Automatically scales your application based on load.                       |
| **Self-Healing**      | Restarts failed containers, replaces and reschedules them when necessary. |
| **Rolling Updates**   | Updates applications with zero downtime.                                   |
| **Service Discovery** | Finds services within the cluster automatically.                          |

---

## ⚙️ Kubernetes Architecture

Kubernetes has a **Master-Worker** architecture:

### 🧠 Control Plane (Master Node)

Manages the cluster. Key components:

- `kube-apiserver`: Entry point for commands.
- `etcd`: Key-value store for cluster state.
- `kube-scheduler`: Assigns Pods to nodes.
- `kube-controller-manager`: Handles controllers (replica, node, endpoints, etc.).
- `cloud-controller-manager`: Manages cloud-specific logic.

### 🧳 Worker Node (Minion)

Runs application workloads. Key components:

- `kubelet`: Communicates with the API server.
- `kube-proxy`: Manages networking.
- `Container Runtime`: Runs containers (Docker, containerd, etc.).

---

## 🧩 Kubernetes Core Concepts

### 1. **Pod**
- Smallest deployable unit in Kubernetes.
- Wraps one or more containers.

### 2. **Deployment**
- Manages the lifecycle of Pods (create, update, rollback).

### 3. **Service**
- Exposes Pods to internal/external traffic.

### 4. **Namespace**
- Logical cluster segmentation for multi-tenancy.

### 5. **ConfigMap & Secret**
- Manage app configuration and sensitive data.

---

## 💡 How Kubernetes Works (Simplified Flow)

1. You define a **Deployment YAML**.
2. `kubectl apply -f deploy.yaml` sends the spec to the API Server.
3. Kubernetes Scheduler decides **where to run the Pod**.
4. **Kubelet** tells the container runtime to run the container.
5. Pod is created and exposed via **Service**.

---

## 📦 Kubernetes vs Docker

| Feature              | Docker                                | Kubernetes                      |
|----------------------|---------------------------------------|----------------------------------|
| Focus                | Containerization                      | Orchestration                    |
| Networking           | Basic via bridge/network              | Advanced Service Discovery       |
| Scaling              | Manual                                | Automatic                        |
| Load Balancing       | Not built-in                          | Built-in                         |
| Self-Healing         | No                                    | Yes                              |

Kubernetes can **run Docker containers**, but it adds powerful orchestration capabilities on top.

---

## 🧪 Getting Started with Kubernetes (Minikube)

```bash
# Start a Kubernetes cluster locally
minikube start

# Check cluster status
kubectl cluster-info

# List nodes
kubectl get nodes

