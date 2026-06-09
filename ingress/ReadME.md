INSTALLING INGRESS-NGINX-CONTROLLER ON EKS 

1. Install helm 
   1. curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash 
   2. helm version

2. Install nginx-ingress using helm
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.type=LoadBalancer \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-type"="nlb" \
  --set controller.replicaCount=2

3. verify 
   1. kubectl get pods -n ingress-nginx 
   2. kubectl get svc -n ingress-nginx 
