# Day 30 - Real-World Kubernetes Deployment Example

Welcome to **Day 30** of our Kubernetes journey! Today, we wrap up everything we've learned by deploying a fully functional, multi-tier application using key Kubernetes concepts from Days 23–29.


[![](https://img.youtube.com/vi/pAsUEqQ1eKI/0.jpg)](https://www.youtube.com/watch?v=pAsUEqQ1eKI)

[Watch the video](https://www.youtube.com/watch?v=pAsUEqQ1eKI)
---

## 🎯 Objective

Deploy a complete **full-stack application** with the following components:

- **Frontend:** React application
- **Backend:** Express.js server exposing a REST API
- **Database:** PostgreSQL
- **Monitoring:** Prometheus + Grafana

---

## 🗂️ Directory Structure

```

capstone/
├── k8s/
│   ├── namespace.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── postgres-deployment.yaml
│   ├── postgres-service.yaml
│   └── configmap.yaml
├── frontend/
│   ├── Dockerfile
│   ├── .env
│   └── \[React App Code]
├── backend/
│   ├── Dockerfile
│   └── \[Express App Code]
└── README.md

````

---

## 🧰 Tools Used

- **Minikube** (local Kubernetes cluster)
- **kubectl** (K8s CLI)
- **Docker** (image builds)
- **Prometheus & Grafana** (monitoring)
- **NodePort & Port Forwarding** for local access

---

## 🔧 Step-by-Step Deployment

### 1. Start Minikube

```bash
minikube start --driver=docker
````

### 2. Create Namespace

```yaml
# k8s/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: capstone-app
```

```bash
kubectl apply -f k8s/namespace.yaml
```

---

### 3. Deploy PostgreSQL

```bash
kubectl apply -f k8s/postgres-deployment.yaml -n capstone-app
kubectl apply -f k8s/postgres-service.yaml -n capstone-app
```

---

### 4. Deploy Backend

```bash
kubectl apply -f k8s/backend-deployment.yaml -n capstone-app
kubectl apply -f k8s/backend-service.yaml -n capstone-app
```

---

### 5. Deploy Frontend

```bash
kubectl apply -f k8s/frontend-deployment.yaml -n capstone-app
kubectl apply -f k8s/frontend-service.yaml -n capstone-app
```

---

### 6. Access Frontend via Port Forwarding

```bash
kubectl port-forward svc/frontend -n capstone-app 32362:80
```

Then visit:
👉 `http://localhost:32362`

---

## ✅ Verifications

* Access Frontend → “Connected to Backend”
* Inspect Network Request to `/api` → should return backend message
* Backend can access PostgreSQL
* All Pods show `STATUS: Running`

---

## 📈 Bonus: Monitoring Setup

Install Prometheus & Grafana using Helm (optional):

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
```

Port forward to access UIs:

```bash
kubectl port-forward svc/prometheus-kube-prometheus-prometheus -n monitoring 9090
kubectl port-forward svc/grafana -n monitoring 3000:80
```

---

## 🧠 Key Concepts Applied

| Concept         | Example Used                   |
| --------------- | ------------------------------ |
| Namespaces      | capstone-app                   |
| Deployments     | frontend, backend, postgres    |
| Services        | ClusterIP & NodePort           |
| ConfigMaps      | React app config via `.env`    |
| Port Forwarding | frontend exposed on port 32362 |
| DNS in Cluster  | `http://backend:3000/api`      |
| Monitoring      | Prometheus scraping services   |

---

## 🎉 Congratulations!

You’ve now built and deployed a complete application using Kubernetes primitives! This project ties together all you've learned from Pods and Deployments to Services, Networking, ConfigMaps, and Observability.

---

## 🧪 Try These Next

* Add Ingress with TLS
* Use PersistentVolumeClaim for PostgreSQL
* Horizontal Pod Autoscaling
* CI/CD pipeline with GitHub Actions and `kubectl apply`

---

> *“The best way to learn Kubernetes is to build real things. You just did. Onward!”*

```

---

