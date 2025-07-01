# **Kubernetes Deployment for Microservices with k3s**

This repository contains Kubernetes configuration files for deploying various services such as **Redis**, **PostgreSQL**, **RabbitMQ**, **Django**, **Next.js**, and **Nginx**. This documentation will guide you through setting up your server, installing **k3s**, and configuring your services. For each service, a detailed configuration guide is available in its corresponding folder.

## **1\. Server Setup and Prerequisites**

Before deploying k3s and its services, you need to configure your server. Follow these steps:

### **Disable Swap**

Swap should be disabled for Kubernetes to function correctly:
```bash
sudo swapoff -a  
sudo sed -i '/ swap / s/^/\#/' /etc/fstab
```

## **2\. Install k3s and Set Up Cluster**

**k3s** is a lightweight, easy-to-install Kubernetes distribution. It includes most necessary components, like a CNI (Container Network Interface) plugin, pre-configured.

### **Initialize k3s Master Node**

To install k3s and initialize your master node, run this command. It will download and install k3s, set up the required services, and configure kubectl for you.
```bash
curl -sfL https://get.k3s.io | sh -
```
After installation, verify it and access your cluster:

```bash
sudo kubectl get nodes
```
You might need to wait a moment for the node to show as Ready.

### **Join Worker Nodes (Optional)**

To add worker nodes to your k3s cluster, you'll need the **Node Token** from your master node. Get the token by running this command on your master:
```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```
On each worker node you want to join, run the following command, replacing \<MASTER\_IP\> with your k3s master node's IP address and \<NODE\_TOKEN\> with the token you obtained:
```bash
curl -sfL https://get.k3s.io | K3S_URL=https://<MASTER_IP>:6443 K3S_TOKEN=<NODE_TOKEN> sh -
```
## **3\. Install Metrics Server**

**Metrics Server** is a scalable, efficient source of container resource metrics for Kubernetes' built-in autoscaling pipelines.

To install Metrics Server, run this command:
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
You can verify that Metrics Server is running by checking the pods in the kube-system namespace. It might take a few moments for the pods to become Running.
```bash
kubectl get pods -n kube-system | grep metrics-server
```
Once installed, you can use kubectl top commands to view resource usage:
```bash
kubectl top nodes  
kubectl top pods --all-namespaces
```
## **4\. Verify Cluster and Node Status**

Check the status of your nodes and pods to ensure everything is running as expected:
```bash
kubectl get nodes  
kubectl get pods --all-namespaces
```
Make sure all nodes show a status of Ready.

## **5\. Link to Service-Specific Documentation**

Now that your k3s cluster is set up and Metrics Server is installed, you can proceed with deploying your services. Follow the links below to the specific services you want to deploy:

* [Redis Configuration and Deployment](./redis/README.md)  
* [PostgreSQL Configuration and Deployment](./postgresql/README.md)  
* [RabbitMQ Configuration and Deployment](./rabbitmq/README.md)  
* [Django Application Configuration and Deployment](./django/README.md)  
* [Next.js Application Configuration and Deployment](./nextjs/README.md)  
* [Nginx Load Balancer Configuration](./nginx/README.md)

Be sure to follow each service's detailed guide to configure and deploy it within your Kubernetes cluster.
