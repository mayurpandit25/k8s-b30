# EasyCRUD

A Three-Tier Application deployed on AWS EKS using Kubernetes, NGINX Ingress Controller, Route 53, and Load Balancer.

## Project Repository

**GitHub Repository:**
https://github.com/mayurpandit25/EasyCRUD

---

# EKS Cluster Creation Using AWS CLI

## 1. Install kubectl

```bash
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.35.3/202604-08/bin/linux/amd64/kubectl

chmod +x ./kubectl

mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH

echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc

kubectl version --client
```

---

## 2. Install eksctl

Official Documentation:

https://docs.aws.amazon.com/eks/latest/eksctl/installation.html

---

## 3. Create EKS Cluster

```bash
eksctl create cluster \
--name eks \
--region us-east-1 \
--version 1.35 \
--nodegroup-name workers \
--node-type c7i-flex.large \
--nodes 2 \
--managed
```

---

## 4. Connect To EKS Cluster

```bash
aws eks update-kubeconfig \
--region us-east-1 \
--name eks
```

Verify Nodes:

```bash
kubectl get nodes
```

---

## 5. Delete EKS Cluster

```bash
eksctl delete cluster \
--name eks \
--region us-east-1
```

---

# Install NGINX Ingress Controller

Deploy Ingress Controller:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/aws/deploy.yaml
```

Verify Pods:

```bash
kubectl get pods -n ingress-nginx
```

Verify Services:

```bash
kubectl get svc -n ingress-nginx
```

---

# Kubernetes Components

### Frontend

* Kubernetes Deployment
* ClusterIP Service

### Backend

* Kubernetes Deployment
* ClusterIP Service

### Database

* Database connected to Backend

### Networking

* NGINX Ingress Controller
* Ingress Rules
* AWS Load Balancer
* Route 53 DNS

---

### Routes

```text
/      -> Frontend
/api   -> Backend
```

---

# Author

**Mayur Pandit**

GitHub: https://github.com/mayurpandit25/EasyCRUD
