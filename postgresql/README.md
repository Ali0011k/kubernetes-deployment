# Postgresql Setup in Kubernetes

This guide will help you set up Postgresql in your Kubernetes cluster, including its **deployment**, **service**, **persistent volume**, **HPA** (Horizontal Pod Autoscaler), and **health checks**.

### Steps:

### 1. **Deploy Postgresql StatefulSet**

create the Postgresql StatefulSet, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f postgresql-statefulset.yaml
```

### 2. **Create Postgresql Service**

Create a service to expose Postgresql within the Kubernetes cluster:

```bash
kubectl apply -f postgresql-service.yaml
```

### 6. **Verify Postgresql Setup**

#### 1. **Check Pods:**
You can check the status of your Postgresql pods to ensure they are running:

```bash
kubectl get pods
```

#### 2. **Check StatefulSet:**
To see the status of the Postgresql StatefulSet:

```bash
kubectl get statefulset postgresql
```

### 3. **Delete Postgresql Resources**

To delete all Postgresql-related resources from the cluster:

```bash
kubectl delete -f postgresql-statefulset.yaml
kubectl delete -f postgresql-service.yaml
```

---

### Notes:
- **StatefulSet** is used because Postgresql requires stable network identity and persistent storage.

By following these steps, Postgresql will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
