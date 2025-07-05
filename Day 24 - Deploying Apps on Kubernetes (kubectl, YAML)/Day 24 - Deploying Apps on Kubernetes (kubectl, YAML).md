# Day 24 - Deploying Apps on Kubernetes (kubectl, YAML)

## 1. What is a Kubernetes Cluster?

A **Kubernetes cluster** is a collection of computers (called nodes) that run containerized applications managed by Kubernetes. It abstracts away the underlying hardware and provides a powerful, scalable, and self-healing platform for running your applications.


[![](https://img.youtube.com/vi/aeXJyxX7j6Y/0.jpg)](https://www.youtube.com/watch?v=aeXJyxX7j6Y)

[Watch the video](https://www.youtube.com/watch?v=aeXJyxX7j6Y)

### Key Components:

- **Control Plane (Master Node)**  
  Responsible for managing the cluster’s state, scheduling workloads, and making global decisions. Key components include:  
  - `kube-apiserver`: API server, the cluster’s front door  
  - `kube-controller-manager`: Runs controller processes  
  - `kube-scheduler`: Assigns workloads to nodes  
  - `etcd`: Distributed key-value store for cluster data

- **Worker Nodes**  
  Run your application containers inside Pods. Each node runs:  
  - `kubelet`: Agent managing containers on a node  
  - `kube-proxy`: Handles network proxying  
  - Container runtime (e.g., Docker, containerd)

---

## 2. Introduction to YAML for Kubernetes

Kubernetes resources are described declaratively using **YAML files**. These files define the desired state of your resources—such as Deployments, Services, ConfigMaps—and Kubernetes works to maintain that state.

### Why YAML?
- Human-readable and easy to write  
- Defines complex objects with nesting and lists  
- Declarative style: You specify *what* you want, not *how* to do it  

---

## 3. How to Write Kubernetes YAML Files

### Basic Structure

Every Kubernetes resource YAML includes these sections:

```yaml
apiVersion: <api-version>
kind: <resource-kind>
metadata:
  name: <resource-name>
  labels:            # optional but recommended
    key: value
spec:
  # resource-specific configuration here
````

### YAML Syntax Rules

* Use **2 spaces** per indentation level (never tabs)
* Use `-` to denote list items
* Strings don’t need quotes unless they contain special characters
* Comments start with `#`

---

## 4. Core Kubernetes Objects Explained

### 4.1 Deployment

A **Deployment** manages Pods and ReplicaSets, providing declarative updates and rollbacks.

**Key Features:**

* Controls the number of Pod replicas
* Enables rolling updates without downtime
* Automatically replaces failed Pods

**Example Deployment YAML:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2                      # desired number of Pods
  selector:                       # label selector to identify Pods managed
    matchLabels:
      app: nginx
  template:                       # Pod template used to create Pods
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

---

### 4.2 ReplicaSet

A **ReplicaSet** ensures that a specified number of identical Pods are running at any time. Deployments create and manage ReplicaSets behind the scenes.

* Typically, you do **not manage ReplicaSets directly**, but it’s important to understand their role in Pod lifecycle management.

---

### 4.3 Service

A **Service** exposes your Pods to network traffic and load balances requests.

**Types of Services:**

* `ClusterIP` (default): Internal access only
* `NodePort`: Exposes service on each Node’s IP at a static port
* `LoadBalancer`: Creates an external load balancer (cloud providers only)

**Example Service YAML:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx                   # select Pods labeled 'app: nginx'
  ports:
    - protocol: TCP
      port: 80                  # port exposed inside the cluster
      targetPort: 80            # port on the Pod container
  type: NodePort                # expose service on each node's port
```

---

## 5. Tools You Need

| Tool       | Purpose                              |
| ---------- | ------------------------------------ |
| `kubectl`  | Kubernetes CLI to manage cluster     |
| `minikube` | Local Kubernetes cluster for testing |

---

## 6. Step-by-Step: Creating a Kubernetes Cluster and Deploying an App

### Step 1: Install `kubectl`

```bash
sudo apt update
sudo apt install -y apt-transport-https curl

curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg \
  https://packages.cloud.google.com/apt/doc/apt-key.gpg

echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] \
  https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install -y kubectl
```

Verify installation:

```bash
kubectl version --client
```

---

### Step 2: Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```bash
minikube version
```

---

### Step 3: Start the Minikube Cluster

```bash
minikube start --driver=docker
```

Check node status:

```bash
kubectl get nodes
```

---

### Step 4: Create `deployment.yaml`

Create a file named `deployment.yaml` with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

### Step 5: Create `service.yaml`

Create a file named `service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```

---

### Step 6: Apply the YAML files

Deploy the app and service:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Check the Deployment and Pods:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

---

### Step 7: Access Your App

Use Minikube to access the service:

```bash
minikube service nginx-service
```

This command opens the NGINX welcome page in your browser.

---

### Step 8: Clean up Resources

To delete your deployment and service:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

Stop Minikube when done:

```bash
minikube stop
```

---

## 7. Best Practices for Writing Kubernetes YAML

| Practice                            | Reason                                       |
| ----------------------------------- | -------------------------------------------- |
| Use consistent 2-space indentation  | YAML syntax requires proper indentation      |
| Use comments (`#`)                  | Makes files easier to understand             |
| Break resources into separate files | Clear organization and easier management     |
| Label your resources properly       | For effective selector matching and grouping |
| Use declarative `kubectl apply`     | Keeps your cluster in sync with YAML         |

---

## 8. Summary and Recap

| Component          | Description                                            |
| ------------------ | ------------------------------------------------------ |
| Kubernetes Cluster | Orchestrates containerized apps with high availability |
| YAML               | Declarative format to define Kubernetes objects        |
| Deployment         | Declaratively manages Pods and ReplicaSets             |
| ReplicaSet         | Ensures specified number of Pods are always running    |
| Service            | Exposes Pods and enables networking and load balancing |

---

## 9. Quick `kubectl` Command Reference

| Task                      | Command                             |
| ------------------------- | ----------------------------------- |
| Apply config              | `kubectl apply -f <filename>.yaml`  |
| Check Deployments         | `kubectl get deployments`           |
| Check Pods                | `kubectl get pods`                  |
| Check Services            | `kubectl get services`              |
| Delete resources          | `kubectl delete -f <filename>.yaml` |
| Access Service (Minikube) | `minikube service <service-name>`   |
