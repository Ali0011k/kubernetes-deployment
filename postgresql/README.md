
# PostgreSQL Setup in Kubernetes

This guide will walk you through setting up PostgreSQL in your Kubernetes cluster, including its deployment, service, persistent volume, HPA (Horizontal Pod Autoscaler), and health checks.

## Steps:

### 1. Create ConfigMap for PostgreSQL Configuration (Optional)
If you want to provide custom configuration settings for PostgreSQL, you can use a ConfigMap. Apply it using:
```bash
kubectl apply -f postgresql-configmap.yaml
```

### 2. Create Persistent Volume Claim (PVC) for PostgreSQL Data Storage
Next, create a Persistent Volume Claim to persist PostgreSQL data:
```bash
kubectl apply -f postgresql-pvc.yaml
```

### 3. Deploy PostgreSQL
Now, create the PostgreSQL Deployment, including health checks such as Liveness and Readiness Probes:
```bash
kubectl apply -f postgresql-deployment.yaml
```

### 4. Create PostgreSQL Service
Create a service to expose PostgreSQL within the Kubernetes cluster:
```bash
kubectl apply -f postgresql-service.yaml
```

### 5. Create Horizontal Pod Autoscaler (HPA)
To enable automatic scaling of PostgreSQL pods based on CPU and memory usage, apply the HPA configuration:
```bash
kubectl apply -f postgresql-hpa.yaml
```

## Verify PostgreSQL Setup:

### 1. Check Pods: You can check the status of your PostgreSQL pods to ensure they are running:
```bash
kubectl get pods
```

### 2. Check Deployment: To see the status of the PostgreSQL deployment:
```bash
kubectl get deployment postgresql
```

### 3. Check HPA: Verify the status of the HPA to ensure it's scaling the pods based on resource usage:
```bash
kubectl get hpa postgresql-hpa
```

## Optional:
### 1. Manually Scale PostgreSQL Deployment: If you need to manually scale the PostgreSQL deployment, you can do so by increasing the number of replicas:
```bash
kubectl scale deployment postgresql --replicas=3
```

### 2. Delete PostgreSQL Resources: To delete all PostgreSQL-related resources from the cluster:
```bash
kubectl delete -f postgresql-deployment.yaml
kubectl delete -f postgresql-service.yaml
kubectl delete -f postgresql-hpa.yaml
kubectl delete -f postgresql-pvc.yaml
kubectl delete -f postgresql-configmap.yaml
```

By following these steps, PostgreSQL will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
