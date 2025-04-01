# Next.js Setup in Kubernetes

This guide will help you set up Next.js in your Kubernetes cluster, including its deployment, service, persistent volume (optional), HPA (Horizontal Pod Autoscaler), and probes for health checks.

## Steps:

### 1. Create ConfigMap for Next.js Configuration (Optional)
Create a ConfigMap to store environment variables for Next.js:
```bash
kubectl apply -f nextjs-configmap.yaml
```

### 2. Deploy Next.js Application
Deploy the Next.js application with Liveness and Readiness Probes:
```bash
kubectl apply -f nextjs-deployment.yaml
```

### 3. Create Next.js Service
Expose the Next.js application within the Kubernetes cluster:
```bash
kubectl apply -f nextjs-service.yaml
```

### 4. Create Horizontal Pod Autoscaler (HPA)
Enable automatic scaling for the Next.js application based on CPU and memory usage:
```bash
kubectl apply -f nextjs-hpa.yaml
```

## Verify Next.js Setup:
### 1. Check Pods: Check the status of your Next.js pods to ensure they are running:
```bash
kubectl get pods
```

### 2. Check Deployment: To see the status of the Next.js deployment:
```bash
kubectl get deployment nextjs
```
### 3. Check HPA: Verify the status of the HPA to ensure it is scaling the pods based on resource usage:
```bash
kubectl get hpa nextjs-hpa
```

## Optional:
### 1. Manually Scale Next.js Deployment: If you need to manually scale the Next.js deployment, you can increase the number of replicas:
```bash
kubectl scale deployment nextjs --replicas=3
```

### 2. Delete Next.js Resources: To delete all Next.js-related resources from the cluster:
```bash
kubectl delete -f nextjs/nextjs-deployment.yaml
kubectl delete -f nextjs/nextjs-service.yaml
kubectl delete -f nextjs/nextjs-hpa.yaml
kubectl delete -f nextjs/nextjs-pvc.yaml
kubectl delete -f nextjs/nextjs-configmap.yaml
```
By following these steps, Next.js will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
