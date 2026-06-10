# Installing NGINX Ingress Controller on EKS

## 1. Install Helm

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Verify Helm installation:

```bash
helm version
```

---

## 2. Install NGINX Ingress using Helm

### Add the Helm Repository

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```

### Install NGINX Ingress Controller

```bash
helm install ingress-nginx ingress-nginx/ingress-nginx \
    --namespace ingress-nginx \
    --create-namespace \
    --set controller.service.type=LoadBalancer \
    --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-type"="nlb" \
    --set controller.replicaCount=2
```

---

## 3. Verify Installation

Check the Ingress Controller Pods:

```bash
kubectl get pods -n ingress-nginx
```

Check the Service and External Load Balancer:

```bash
kubectl get svc -n ingress-nginx
```

Expected Output:

* Pods should be in the **Running** state.
* The `ingress-nginx-controller` service should have an **EXTERNAL-IP** (AWS NLB DNS name).
