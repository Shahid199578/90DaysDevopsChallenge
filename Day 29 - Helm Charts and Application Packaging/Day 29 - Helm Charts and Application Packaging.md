# Day 29 - Helm Charts and Application Packaging

[![](https://img.youtube.com/vi/HG38LO5K8tA/0.jpg)](https://www.youtube.com/watch?v=HG38LO5K8tA)

[Watch the video](https://www.youtube.com/watch?v=HG38LO5K8tA)

Welcome to **Day 29** of the #90DaysOfDevOps challenge!  
Today, we dive into the world of **Helm**, the package manager for Kubernetes.

---

## 📌 Why Helm?

Managing Kubernetes apps involves a lot of YAML — `Deployment`, `Service`, `ConfigMap`, `PVC`, etc.  
For a **microservices architecture**, this quickly becomes overwhelming.

Helm solves this by:
- Packaging everything into a single unit called a **Chart**
- Enabling **templating**, **versioning**, and **reuse**
- Simplifying **deployments**, **upgrades**, and **rollbacks**

---

## 📦 What is a Helm Chart?

A Helm Chart is a collection of files that describe a related set of Kubernetes resources.

```

myapp/
├── Chart.yaml          # Chart metadata
├── values.yaml         # Default configuration values
└── templates/          # Templated Kubernetes manifests
├── deployment.yaml
├── service.yaml
├── configmap.yaml
└── \_helpers.tpl    # Optional: reusable template helpers

````

---

## 🛠️ Installing Helm

### 🔧 Install Helm CLI
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
````

Or use a package manager:

* macOS: `brew install helm`
* Ubuntu: `sudo apt install helm`

### ✅ Verify Installation

```bash
helm version
```

---

## 🎮 Using Helm with Minikube (Even on EC2!)

1. SSH into your EC2 where Minikube is running:

   ```bash
   ssh -i your-key.pem ec2-user@your-ec2-public-ip
   ```

2. Create or install a chart:

   ```bash
   helm repo add bitnami https://charts.bitnami.com/bitnami
   helm install my-nginx bitnami/nginx
   ```

3. Access via port-forwarding:

   ```bash
   kubectl port-forward svc/my-nginx 8080:80
   ```

   Now open `http://<your-ec2-ip>:8080`

---

## 🔄 Rollback a Helm Release

1. Check revision history:

   ```bash
   helm history my-nginx
   ```

2. Rollback:

   ```bash
   helm rollback my-nginx 1
   ```

---

## 🧪 Bonus: Create Your Own Chart

```bash
helm create myapp
```

Edit `values.yaml` and files under `templates/`, then deploy:

```bash
helm install myapp ./myapp
```

---

## 🧠 Best Practices

* Use `values.yaml` for config separation
* Version your charts (semver)
* Use `_helpers.tpl` to avoid repetition
* Store charts in a versioned repository (e.g., GitHub Pages, ChartMuseum)

## 🔗 Resources

* [Helm Docs](https://helm.sh/docs/)
* [Bitnami Charts](https://bitnami.com/stacks/helm)
* [Helm Charts GitHub](https://github.com/helm/charts)

---

✅ **Day 29 Completed!** You're now ready to package and manage your K8s apps with confidence using Helm!
Tag your progress: `#90DaysOfDevOps`

