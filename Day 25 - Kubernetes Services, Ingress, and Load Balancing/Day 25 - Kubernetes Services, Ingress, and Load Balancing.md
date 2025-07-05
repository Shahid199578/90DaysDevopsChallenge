# Day 25 - Kubernetes Services, Ingress, and Load Balancing
Welcome to Day 25 of the 90 Days of DevOps Challenge! Today we’re diving into how networking works in Kubernetes with **Services**, **Ingress**, and **Load Balancing**.


[![](https://img.youtube.com/vi/AWHPZrwjUeU/0.jpg)](https://www.youtube.com/watch?v=AWHPZrwjUeU)

[Watch the video](https://www.youtube.com/watch?v=AWHPZrwjUeU)



---

## 🧩 Why Do We Need Services?

Pods in Kubernetes are **ephemeral** — they can be destroyed and recreated at any time, leading to changes in their IP addresses. To ensure **stable access** to Pods, Kubernetes introduces **Services**.

---

## 🚪 Kubernetes Services – Overview

A **Service** is an abstraction that defines a **logical set of Pods** and a policy by which to access them.

### 🔧 Types of Services

| Type           | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| **ClusterIP**  | Default. Exposes service on an internal IP (within the cluster).           |
| **NodePort**   | Exposes the service on a static port on each node's IP.                    |
| **LoadBalancer** | Uses external load balancer (cloud environments).                        |
| **ExternalName** | Maps service to a DNS name.                                               |
| **Headless**   | No cluster IP, allows direct access to Pods via DNS.                       |

---

## 🧪 Example: NodePort Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
````

```bash
kubectl apply -f service.yaml
minikube service my-nginx-service
```

---

## 🌍 Ingress in Kubernetes

An **Ingress** is an API object that manages **external access** to services, typically HTTP.

It acts as a **reverse proxy** and **routes traffic** based on host/path.

### 🔧 Ingress Controller

To use Ingress, an **Ingress Controller** must be deployed (e.g., `nginx-ingress`, `traefik`, etc.).

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
```

---

### 🧪 Ingress Resource Example

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
    - host: myapp.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-nginx-service
                port:
                  number: 80
```

**Update /etc/hosts**:

```
127.0.0.1 myapp.local
```

---

## ⚖️ Load Balancing in Kubernetes

Kubernetes supports multiple load balancing strategies:

### 🔸 Internal (Service-level)

* Round-robin traffic to Pods via Services.

### 🔸 External

* Cloud Load Balancers via `type: LoadBalancer`.

### 🔸 Ingress Controller

* Provides HTTP layer 7 routing and balancing.

---

## 🧠 Flow Recap

1. **Pod** is deployed.
2. **Service** groups Pods and provides stable access.
3. **Ingress** routes external HTTP(S) traffic to Services.
4. **LoadBalancer/Ingress Controller** enables internet access.

---

## ✅ Summary

* Services enable stable access to dynamic Pods.
* NodePort and LoadBalancer expose apps externally.
* Ingress simplifies HTTP/S routing with hostname and path rules.
* Ingress Controllers must be installed separately.

