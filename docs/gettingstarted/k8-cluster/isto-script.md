---
sidebar_position: 0
sidebar_label: Istio-Script
---
# Istio Installation Script

## Istion Install Script

```bash
# deploy namespaces
kubectl create namespace default
kubectl create namespace frontend
kubectl create namespace backend
kubectl create namespace database

# Get istio
curl -L https://istio.io/downloadIstio | sh -

export PATH="$PATH:/home/admin01/istio-1.13.3/bin"

# validate
istioctl x precheck

# insall istio
istioctl install

# when you see Proceed? (y/N) 
y


istioctl operator init --watchedNamespaces=istio-system,default,frontend,backend,database

# inject envoy
kubectl label namespace default istio-injection=enabled
kubectl label namespace frontend istio-injection=enabled
kubectl label namespace backend istio-injection=enabled
kubectl label namespace database istio-injection=enabled
kubectl apply -f istio-1.13.3/samples/addons

# deploy cert-manager
helm repo add jetstack https://charts.jetstack.io

# update
helm repo update

# deploy cert-manager
helm install \
 cert-manager jetstack/cert-manager \
 --namespace cert-manager \
 --create-namespace \
 --version v1.8.0 \
 --set installCRDs=true

# deploy letsencrypt app.carelyo.in
kubectl apply -f deployment/istio-app/cert-manager/app.carelyo.in.yaml

# staging issuer
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

# deploy app secrets
kubectl apply -f deployment/istio-app/secrets/

# deploy access log
istioctl install --set meshConfig.accessLogFile=/dev/stdout

#Proceed? (y/N) 
y

# deploy gateway
kubectl apply -f deployment/istio-app/login/gateway.yaml

# deploy virtualservices
kubectl apply -f deployment/istio-app/login/virtualservice.yaml

# deploy app
kubectl apply -f deployment/istio-app/login/database.yaml
kubectl apply -f deployment/istio-app/login/login.yaml
kubectl apply -f deployment/istio-app/login/registration-svr.yaml
kubectl apply -f deployment/istio-app/login/authorization.yaml
```