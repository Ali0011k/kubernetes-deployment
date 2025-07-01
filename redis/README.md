
# Redis Setup in Kubernetes

This guide will help you set up Redis in your Kubernetes cluster, including its **deployment**, **service**, **persistent volume**, **HPA** (Horizontal Pod Autoscaler), and **health checks**.

### Steps:


### 1. **Deploy Redis Deployment**

create the Redis Deployment, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f redis-deployment.yaml
```

### 2. **Create Redis Service**

Create a service to expose Redis within the Kubernetes cluster:

```bash
kubectl apply -f redis-service.yaml
```

### 3. **Create Horizontal Pod Autoscaler (HPA)**

To enable automatic scaling of Redis pods based on CPU usage, apply the HPA configuration:

```bash
kubectl apply -f redis-hpa.yaml
```

### 4. **Verify Redis Setup**

#### 1. **Check Pods:**
You can check the status of your Redis pods to ensure they are running:

```bash
kubectl get pods
```

#### 2. **Check HPA:**
Verify the status of the HPA to ensure it's scaling the pods based on the resource usage:

```bash
kubectl get hpa redis
```

### 5. **Optional: Manually Scale Redis StatefulSet**

If you need to manually scale the Redis StatefulSet, you can do so by increasing the number of replicas:

```bash
kubectl scale statefulset redis --replicas=3
```

### 6. **Delete Redis Resources**

To delete all Redis-related resources from the cluster:

```bash
kubectl delete -f redis-deployment.yaml
kubectl delete -f redis-service.yaml
kubectl delete -f redis-hpa.yaml
```

---

### Notes:
- **Horizontal Pod Autoscaler (HPA)** will allow Redis to automatically scale based on CPU and memory utilization.

By following these steps, Redis will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
