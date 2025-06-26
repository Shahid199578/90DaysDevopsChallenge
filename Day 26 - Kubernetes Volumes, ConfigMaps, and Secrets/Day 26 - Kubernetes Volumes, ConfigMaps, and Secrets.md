# Day 26 – Kubernetes Volumes, ConfigMaps, and Secrets

**Date:** June 26, 2025

## 🎯 Objectives
- Understand the concept of Kubernetes Volumes and their types.
- Learn how to use ConfigMaps for configuration management.
- Explore Secrets to manage sensitive data securely.

---

## 📦 Kubernetes Volumes

Volumes in Kubernetes are used to persist data across container restarts.

### Why Volumes?
- Containers are ephemeral.
- Data stored inside a container is lost if the container crashes or is restarted.
- Volumes allow data to be shared among containers in a pod and persist beyond container life.

### Common Volume Types:
- `emptyDir`: For temporary scratch space shared between containers.
- `hostPath`: Maps a file or directory from the host node's filesystem into the Pod.
- `persistentVolumeClaim` (PVC): Used to request storage from a PersistentVolume.

### Example: `emptyDir`
```yaml
volumes:
  - name: cache-volume
    emptyDir: {}
```

---

## ⚙️ ConfigMaps

ConfigMaps are used to inject configuration data into Pods.

### Use Cases:
- Store non-sensitive configuration values (e.g., environment variables, command-line arguments).
- Decouple configuration from application code.

### Create ConfigMap:
```bash
kubectl create configmap app-config --from-literal=APP_MODE=production
```

### Mount into Pod:
```yaml
envFrom:
  - configMapRef:
      name: app-config
```

---

## 🔐 Secrets

Secrets are similar to ConfigMaps but intended for sensitive data like passwords, tokens, or keys.

### Key Characteristics:
- Stored in base64-encoded format (not encrypted by default).
- Must be accessed securely with RBAC and proper usage patterns.

### Create a Secret:
```bash
kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=secret123
```

### Use in Pod:
```yaml
env:
  - name: DB_USER
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: username
```

---

## 🔐 Security Note

While Secrets are stored base64-encoded, this is **not secure encryption**. Use Kubernetes RBAC and tools like HashiCorp Vault for enhanced security in production.

---

## ✅ Summary

- Volumes persist data beyond container life.
- ConfigMaps allow external configuration of applications.
- Secrets manage sensitive data with base64 encoding (and should be protected properly).

---
