# Kubernetes Deployment for Microservices

This repository contains Kubernetes configuration files for deploying various services such as Redis, PostgreSQL, RabbitMQ, Django, Next.js, and Nginx. This documentation will guide you through setting up the server, installing Kubernetes, and configuring services. For each service, a detailed configuration guide is available in the corresponding folder.

## 1. Server Setup and Prerequisites

Before deploying Kubernetes and its services, you need to configure your server. Follow these steps to configure your server for Kubernetes.

### Disable Swap
Swap should be disabled to allow Kubernetes to work properly:
```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```
### Configure Kernel Settings for Kubernetes
Run the following commands to configure the necessary kernel modules and sysctl settings for Kubernetes:
```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sudo sysctl --system
```
## 2. Install Docker and Kubernetes Dependencies
Install Docker, which is required for running containers in Kubernetes, and the necessary Kubernetes packages:
```bash
sudo apt update && sudo apt install -y docker.io
sudo systemctl enable --now docker

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update && sudo apt install -y kubelet kubeadm kubectl
sudo systemctl enable --now kubelet
```
## 3. Set Up Kubernetes Cluster
### Initialize Master Node
Run the following command to initialize the Kubernetes master node:
```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
After the initialization is complete, configure `kubectl` to access the cluster:
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
### Join Worker Nodes
To join worker nodes to the cluster, run the following command on each worker node (replace `<TOKEN>` and `<HASH>` with the appropriate values from the master node output):
```bash
sudo kubeadm join <MASTER_IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```
## 4. Install CNI (Network Plugin) for Kubernetes
Now, install a CNI plugin to allow communication between pods. In this setup, we use Flannel as the CNI network plugin:
```bash
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```
## 5. Verify Cluster and Node Status
Check the status of the nodes and pods:
```bash
kubectl get nodes
kubectl get pods --all-namespaces
```
Ensure all nodes show a status of `Ready`.
## 6. Link to Service-Specific Documentation
Now that the Kubernetes cluster is set up, you can follow the links to the specific services you want to deploy.
- [Redis Configuration and Deployment](./redis/README.md)
- [PostgreSQL Configuration and Deployment](./postgresql/README.md)
- [RabbitMQ Configuration and Deployment](./rabbitmq/README.md)
- [Django Application Configuration and Deployment](./django/README.md)
- [Next.js Application Configuration and Deployment](./nextjs/README.md)
- [Nginx Load Balancer Configuration](./nginx/README.md)

Make sure to follow each service's detailed guide to configure and deploy the respective service within the Kubernetes cluster.
