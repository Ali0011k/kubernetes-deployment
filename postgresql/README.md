# Postgresql Setup in Kubernetes

This guide will help you set up Postgresql in your Kubernetes cluster, including its **deployment**, **service**, **persistent volume**, **HPA** (Horizontal Pod Autoscaler), and **health checks**.

### Steps:
### 1. **Create ConfigMap for Postgresql Configuration (Optional)**

If you want to provide custom configuration settings for Postgresql, you can use a ConfigMap. Apply it using:

```bash
kubectl apply -f postgresql-configmap.yaml
```

### 2. **Create Persistent Volume Claim (PVC) for Postgresql Data Storage**

Next, create a Persistent Volume Claim to persist Postgresql data:

```bash
kubectl apply -f postgresql-pvc.yaml
```

### 3. **Deploy Postgresql StatefulSet**

Now, create the Postgresql StatefulSet, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f postgresql-statefulset.yaml
```

### 4. **Create Postgresql Service**

Create a service to expose Postgresql within the Kubernetes cluster:

```bash
kubectl apply -f postgresql-service.yaml
```

### 5. **Create Horizontal Pod Autoscaler (HPA)**

To enable automatic scaling of Postgresql pods based on CPU and memory usage, apply the HPA configuration:

```bash
kubectl apply -f postgresql-hpa.yaml
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

#### 3. **Check HPA:**
Verify the status of the HPA to ensure it's scaling the pods based on the resource usage:

```bash
kubectl get hpa postgresql
```

### 7. **Optional: Manually Scale Postgresql StatefulSet**

If you need to manually scale the Postgresql StatefulSet, you can do so by increasing the number of replicas:

```bash
kubectl scale statefulset postgresql --replicas=3
```

### 8. **Delete Postgresql Resources**

To delete all Postgresql-related resources from the cluster:

```bash
kubectl delete -f postgresql-statefulset.yaml
kubectl delete -f postgresql-service.yaml
kubectl delete -f postgresql-hpa.yaml
kubectl delete -f postgresql-pvc.yaml
kubectl delete -f postgresql-configmap.yaml
```

---

### Notes:
- **StatefulSet** is used because Postgresql requires stable network identity and persistent storage.
- **Horizontal Pod Autoscaler (HPA)** will allow Postgresql to automatically scale based on CPU and memory utilization.
- **ConfigMap** is used to configure Postgresql and **Secret** for securely managing the Postgresql password.

By following these steps, Postgresql will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
