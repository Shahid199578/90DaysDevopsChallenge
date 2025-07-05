# Day 27 - Kubernetes Monitoring (Prometheus + Grafana)


[![](https://img.youtube.com/vi/JHNInajXAt4/0.jpg)](https://www.youtube.com/watch?v=JHNInajXAt4)

[Watch the video](https://www.youtube.com/watch?v=JHNInajXAt4)

## 🎯 Objectives

- Understand Kubernetes monitoring fundamentals.
- Deploy Prometheus and Grafana manually using manifests (no Helm).
- Visualize and explore metrics.
- Set up basic alerts using PrometheusRules.

---

## 📚 Topics Covered

### ✅ Why Monitoring Matters
- Track health and performance of cluster and workloads.
- Gain visibility into CPU, memory, disk, and network.
- Set alerts for critical issues and auto-scale based on metrics.

---

## 🔧 Tools Overview

### Prometheus
- Time-series database that scrapes and stores metrics.
- Works using a **pull model**.
- Uses **PromQL** for queries.

### Grafana
- Visualization layer for Prometheus and other sources.
- Provides real-time dashboards and alerting UI.

---

## 📦 Setup Without Helm

We will manually apply Kubernetes manifests to deploy Prometheus and Grafana.

---

## Step 1️⃣: Create Monitoring Namespace

```bash
kubectl create namespace monitoring
````

---

## Step 2️⃣: Deploy Prometheus

### 1. Create Prometheus ConfigMap

```yaml
# prometheus-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
  namespace: monitoring
  labels:
    name: prometheus-config
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s

    scrape_configs:
      - job_name: 'kubernetes-nodes'
        static_configs:
          - targets: ['localhost:9100']
```

Apply it:

```bash
kubectl apply -f prometheus-config.yaml
```

### 2. Create Prometheus Deployment & Service

```yaml
# prometheus-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prometheus
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
  template:
    metadata:
      labels:
        app: prometheus
    spec:
      containers:
        - name: prometheus
          image: prom/prometheus
          args:
            - "--config.file=/etc/prometheus/prometheus.yml"
          ports:
            - containerPort: 9090
          volumeMounts:
            - name: config-volume
              mountPath: /etc/prometheus/
      volumes:
        - name: config-volume
          configMap:
            name: prometheus-config
```

```yaml
# prometheus-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: prometheus
  namespace: monitoring
spec:
  selector:
    app: prometheus
  ports:
    - port: 9090
      targetPort: 9090
      protocol: TCP
```

Apply:

```bash
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-service.yaml
```

---

## Step 3️⃣: Deploy Grafana

### 1. Create Grafana Deployment

```yaml
# grafana-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana
          image: grafana/grafana
          ports:
            - containerPort: 3000
```

### 2. Create Grafana Service

```yaml
# grafana-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: grafana
  namespace: monitoring
spec:
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
```

Apply:

```bash
kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml
```

---

## 🔌 Access the Dashboards

### Port Forward

```bash
kubectl port-forward svc/prometheus 9090:9090 -n monitoring
kubectl port-forward svc/grafana 3000:3000 -n monitoring
```

* Prometheus: [http://localhost:9090](http://localhost:9090)
* Grafana: [http://localhost:3000](http://localhost:3000)

### Grafana Default Login

* **Username**: `admin`
* **Password**: `admin` (change after first login)

---

## 📊 Configure Prometheus in Grafana

1. Go to Grafana → Settings → Data Sources → Add Data Source.
2. Choose **Prometheus**.
3. URL: `http://prometheus:9090` (internal) or `http://localhost:9090` (via port-forward).
4. Click **Save & Test**.

---

## 📈 Create Dashboards

* Use built-in or community dashboards (e.g. ID: `1860` or `6417` from [grafana.com/dashboards](https://grafana.com/grafana/dashboards)).
* Add panels for:

  * Node metrics
  * Pod memory and CPU
  * Uptime and restarts

---

## 🚨 Example Alerting Rule (Optional)

```yaml
# prometheus-alert-rule.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: example-alert
  namespace: monitoring
spec:
  groups:
  - name: example
    rules:
    - alert: HighMemoryUsage
      expr: container_memory_usage_bytes > 500000000
      for: 1m
      labels:
        severity: warning
      annotations:
        summary: "Memory usage above 500MB"
        description: "Container {{ $labels.container }} using too much memory"
```

> Alertmanager needs to be deployed separately for alerts to work end-to-end.

---

## 🧹 Cleanup

```bash
kubectl delete namespace monitoring
```

---

## 🧠 Summary

* Deployed Prometheus and Grafana manually.
* Exposed services using port-forwarding.
* Configured Prometheus in Grafana.
* Created dashboards and viewed live metrics.
* Discussed basic alert rules.

---


