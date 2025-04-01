# Setting Up Load Balancer with Nginx in Kubernetes

This guide explains how to set up a Load Balancer with Nginx in Kubernetes to manage traffic across different services (like **Next.js** and **Django**) with different domains.

## Steps:

### 1. Create Nginx Service with LoadBalancer Type
First, create a Kubernetes service of type `LoadBalancer` for Nginx to distribute traffic to the appropriate pods.

```bash
kubectl apply -f nginx-service.yaml
```
This will create a Load Balancer service that exposes the Nginx pods externally.

### 2. Configure Nginx for Multiple Domains
Create an Nginx configuration file to route traffic to different services (Next.js and Django) based on the domain.

```bash
kubectl apply -f nginx-configmap.yaml
```

The nginx-configmap.yaml file contains the configuration to route traffic for frontend.yourdomain.com to Next.js and backend.yourdomain.com to Django.

### 3. Deploy Nginx in Kubernetes
After applying the above configurations, deploy the Nginx application in your Kubernetes cluster.

```bash
kubectl apply -f nginx/nginx-deployment.yaml
```
This will create the necessary Nginx pods in your cluster.

### 4. Verify the Load Balancer
To check the status of your Load Balancer and get the external IP, use the following command:
```bash
kubectl get services
```
You should see an external IP assigned to the nginx-lb service.

### 5. Configure DNS Records
Once you have the external IP for your Load Balancer, update your DNS records:

Point frontend.yourdomain.com to the Load Balancer's external IP.

Point backend.yourdomain.com to the same external IP.

This will allow you to access your services using different domains.

## Optional:
### 1. Manually Scale Nginx Deployment
If you need to scale Nginx to handle more traffic, you can manually increase the number of replicas:
```bash
kubectl scale deployment nginx --replicas=3
```

### 2. Delete Nginx Resources
To delete all resources related to Nginx from the cluster, run the following commands:
```bash
kubectl delete -f nginx/nginx-deployment.yaml
kubectl delete -f nginx/nginx-service.yaml
kubectl delete -f nginx/nginx-configmap.yaml
```
## Conclusion:
By following these steps, you'll have a Load Balancer in place with Nginx routing traffic based on domain names to different services like Next.js and Django in your Kubernetes cluster.
