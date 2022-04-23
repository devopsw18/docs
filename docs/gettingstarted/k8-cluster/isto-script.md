---
sidebar_position: 0
sidebar_label: Istio
---
# Istio Installation Script

## Istion Install Script
```bash
kubectl create namespace default
kubectl create namespace frontend
kubectl create namespace backend
kubectl create namespace database
curl -L https://istio.io/downloadIstio | sh -
export PATH="$PATH:/home/admin01/istio-1.13.3/bin"
istioctl x precheck
istioctl install
istioctl operator init --watchedNamespaces=istio-system,default,frontend,backend,database
kubectl label namespace default istio-injection=enabled
kubectl label namespace frontend istio-injection=enabled
kubectl label namespace backend istio-injection=enabled
kubectl label namespace database istio-injection=enabled
kubectl apply -f istio-1.13.3/samples/addons

# deploy cert-manager
helm repo add jetstack https://charts.jetstack.io
helm repo update

helm install \
 cert-manager jetstack/cert-manager \
 --namespace cert-manager \
 --create-namespace \
 --version v1.8.0 \
 --set installCRDs=true

# deploy letsencrypt
kubectl apply -f deployment/istio-app/cert-manager/app.carelyo.in.yaml
kubectl apply -f deployment/istio-app/cert-manager/staging-cluster.yaml


# Secret in namespaces
kubectl -n frontend create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

kubectl -n backend create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

kubectl -n database create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

kubectl apply -f deployment/istio-app/secret/

# deploy apps
kubectl apply -f deployment/istio-app/login/accesslog.yaml
kubectl apply -f deployment/istio-app/login/gateway.yaml
kubectl apply -f deployment/istio-app/login/virtualservice.yaml
kubectl apply -f deployment/istio-app/login/database.yaml
kubectl apply -f deployment/istio-app/login/login.yaml
kubectl apply -f deployment/istio-app/login/registration-svr.yaml
kubectl apply -f deployment/istio-app/login/authorization.yaml




```