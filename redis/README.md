
# Redis Setup in Kubernetes

This guide will help you set up Redis in your Kubernetes cluster, including its deployment, service, persistent volume, HPA (Horizontal Pod Autoscaler), and probes for health checks.

## Steps:

### 1. Create ConfigMap for Redis Configuration (Optional)

If you want to provide custom configuration settings for Redis, you can use a ConfigMap. Apply it using:

```bash
kubectl apply -f redis-configmap.yaml
```

### 2. Create Persistent Volume Claim (PVC) for Redis Data Storage

Next, create a Persistent Volume Claim to persist Redis data:

```bash
kubectl apply -f redis-pvc.yaml
```

### 3. Deploy Redis

Now, create the Redis Deployment, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f redis-deployment.yaml
```

### 4. Create Redis Service

Create a service to expose Redis within the Kubernetes cluster:

```bash
kubectl apply -f redis-service.yaml
```

### 5. Create Horizontal Pod Autoscaler (HPA)

To enable automatic scaling of Redis pods based on CPU and memory usage, apply the HPA configuration:

```bash
kubectl apply -f redis-hpa.yaml
```

## Verify Redis Setup:

### 1. Check Pods: You can check the status of your Redis pods to ensure they are running:

```bash
kubectl get pods
```

### 2. Check Deployment: To see the status of the Redis deployment:

```bash
kubectl get deployment redis
```

### 3. Check HPA: Verify the status of the HPA to ensure it's scaling the pods based on the resource usage:

```bash
kubectl get hpa redis-hpa
```

## Optional:

### 1. Manually Scale Redis Deployment: If you need to manually scale the Redis deployment, you can do so by increasing the number of replicas:

```bash
kubectl scale deployment redis --replicas=3
```

### 2. Delete Redis Resources: To delete all Redis-related resources from the cluster:

```bash
kubectl delete -f redis-deployment.yaml
kubectl delete -f redis-service.yaml
kubectl delete -f redis-hpa.yaml
kubectl delete -f redis-pvc.yaml
kubectl delete -f redis-configmap.yaml
```

By following these steps, Redis will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
