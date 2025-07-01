# Django Setup in Kubernetes

This guide will help you set up Django in your Kubernetes cluster, including its deployment, service, HPA (Horizontal Pod Autoscaler), and probes for health checks.

## Steps:

### 1. Deploy Django Application
Create the Django Deployment, including health checks (Liveness and Readiness Probes):
```bash
kubectl apply -f django-deployment.yaml
```

### 2. Create Django Service
Expose Django within the Kubernetes cluster by creating a service:
```bash
kubectl apply -f django-service.yaml
```

### 3. Create Horizontal Pod Autoscaler (HPA)
Enable automatic scaling of Django pods based on CPU And RAM usage:
```bash
kubectl apply -f django-hpa.yaml
```

## Verify Django Setup:
### 1. Check Pods: You can check the status of your Django pods to ensure they are running:
```bash
kubectl get pods
```

### 2. Check Deployment: To see the status of the Django deployment:
```bash
kubectl get deployment django
```

### 3. Check HPA: Verify the status of the HPA to ensure it's scaling the pods based on resource usage:
```bash
kubectl get hpa django-hpa
```

## Optional:
### 1. Manually Scale Django Deployment: If you need to manually scale the Django deployment, you can do so by increasing the number of replicas:
```bash
kubectl scale deployment django --replicas=3
```

### 2. Delete Django Resources: To delete all Django-related resources from the cluster:
```bash
kubectl delete -f django/django-deployment.yaml
kubectl delete -f django/django-service.yaml
kubectl delete -f django/django-hpa.yaml
```
By following these steps, Django will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
