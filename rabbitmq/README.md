# RabbitMQ Setup in Kubernetes

This guide will help you set up RabbitMQ in your Kubernetes cluster, including its **deployment**, **service**, **persistent volume**, **HPA** (Horizontal Pod Autoscaler), and **health checks**.

### Steps:
### 1. **Create ConfigMap for RabbitMQ Configuration (Optional)**

If you want to provide custom configuration settings for RabbitMQ, you can use a ConfigMap. Apply it using:

```bash
kubectl apply -f rabbitmq-configmap.yaml
```

### 2. **Create Persistent Volume Claim (PVC) for RabbitMQ Data Storage**

Next, create a Persistent Volume Claim to persist RabbitMQ data:

```bash
kubectl apply -f rabbitmq-pvc.yaml
```

### 3. **Deploy RabbitMQ StatefulSet**

Now, create the RabbitMQ StatefulSet, including health checks such as Liveness and Readiness Probes:

```bash
kubectl apply -f rabbitmq-statefulset.yaml
```

### 4. **Create RabbitMQ Service**

Create a service to expose RabbitMQ within the Kubernetes cluster:

```bash
kubectl apply -f rabbitmq-service.yaml
```

### 5. **Create Horizontal Pod Autoscaler (HPA)**

To enable automatic scaling of RabbitMQ pods based on CPU and memory usage, apply the HPA configuration:

```bash
kubectl apply -f rabbitmq-hpa.yaml
```

### 6. **Verify RabbitMQ Setup**

#### 1. **Check Pods:**
You can check the status of your RabbitMQ pods to ensure they are running:

```bash
kubectl get pods
```

#### 2. **Check StatefulSet:**
To see the status of the RabbitMQ StatefulSet:

```bash
kubectl get statefulset rabbitmq
```

#### 3. **Check HPA:**
Verify the status of the HPA to ensure it's scaling the pods based on the resource usage:

```bash
kubectl get hpa rabbitmq
```

### 7. **Optional: Manually Scale RabbitMQ StatefulSet**

If you need to manually scale the RabbitMQ StatefulSet, you can do so by increasing the number of replicas:

```bash
kubectl scale statefulset rabbitmq --replicas=3
```

### 8. **Delete RabbitMQ Resources**

To delete all RabbitMQ-related resources from the cluster:

```bash
kubectl delete -f rabbitmq-statefulset.yaml
kubectl delete -f rabbitmq-service.yaml
kubectl delete -f rabbitmq-hpa.yaml
kubectl delete -f rabbitmq-pvc.yaml
kubectl delete -f rabbitmq-configmap.yaml
```

---

### Notes:
- **StatefulSet** is used because RabbitMQ requires stable network identity and persistent storage.
- **Horizontal Pod Autoscaler (HPA)** will allow RabbitMQ to automatically scale based on CPU and memory utilization.
- **ConfigMap** is used to configure RabbitMQ and **Secret** for securely managing the RabbitMQ password.

By following these steps, RabbitMQ will be successfully set up in your Kubernetes cluster, with automatic scaling and health checks enabled.
