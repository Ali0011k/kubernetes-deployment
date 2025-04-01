
# Redis Setup in Kubernetes

This guide will help you set up Redis in your Kubernetes cluster, including its **deployment**, **service**, **persistent volume**, **HPA** (Horizontal Pod Autoscaler), and **health checks**.

### Steps:
### 1. **Create ConfigMap for Redis Configuration (Optional)**

If you want to provide custom configuration settings for Redis, you can use a ConfigMap. Apply it using:

```bash
kubectl apply -f redis-configmap.yaml
```

### 2. **Create Persistent Volume Claim (PVC) for Redis Data Storage**

Next, create a Persistent Volume Claim to persist Redis data:

```bash
kubectl apply -f redis-pvc.yaml
```

### 3. **Deploy Redis StatefulSet**

Now, create the Redis StatefulSet, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f redis-statefulset.yaml
```

### 4. **Create Redis Service**

Create a service to expose Redis within the Kubernetes cluster:

```bash
kubectl apply -f redis-service.yaml
```

### 5. **Create Horizontal Pod Autoscaler (HPA)**

To enable automatic scaling of Redis pods based on CPU and memory usage, apply the HPA configuration:

```bash
kubectl apply -f redis-hpa.yaml
```

### 6. **Verify Redis Setup**

#### 1. **Check Pods:**
You can check the status of your Redis pods to ensure they are running:

```bash
kubectl get pods
```

#### 2. **Check StatefulSet:**
To see the status of the Redis StatefulSet:

```bash
kubectl get statefulset redis
```

#### 3. **Check HPA:**
Verify the status of the HPA to ensure it's scaling the pods based on the resource usage:

```bash
kubectl get hpa redis
```

### 7. **Optional: Manually Scale Redis StatefulSet**

If you need to manually scale the Redis StatefulSet, you can do so by increasing the number of replicas:

```bash
kubectl scale statefulset redis --replicas=3
```

### 8. **Delete Redis Resources**

To delete all Redis-related resources from the cluster:

```bash
kubectl delete -f redis-statefulset.yaml
kubectl delete -f redis-service.yaml
kubectl delete -f redis-hpa.yaml
kubectl delete -f redis-pvc.yaml
kubectl delete -f redis-configmap.yaml
```

---

### Notes:
- **StatefulSet** is used because Redis requires stable network identity and persistent storage.
- **Horizontal Pod Autoscaler (HPA)** will allow Redis to automatically scale based on CPU and memory utilization.
- **ConfigMap** is used to configure Redis and **Secret** for securely managing the Redis password.

By following these steps, Redis will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
