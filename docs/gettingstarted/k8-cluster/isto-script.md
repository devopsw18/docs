---
sidebar_position: 0
sidebar_label: Istio-Script
---
# Istio Installation Script

## Istio Install Script

```bash
# deploy namespaces
kubectl create namespace frontend
kubectl create namespace backend
kubectl create namespace database
```

```bash
# Get istio
curl -L https://istio.io/downloadIstio | sh -
```
# Export the path
```bash
export PATH="$PATH:/home/admin01/istio-1.13.3/bin"
```
# or 
```bash
cd istio-1.13.3
sudo cp bin/istiocli /usr/local/bin/istiocli
```

```bash
# validate
istioctl x precheck
```

```bash
# insall istio
istioctl install
```
# when you see Proceed? (y/N)
```bash 
y
```
# Install istio operator which automate updates etc. of istio 
```bash
istioctl operator init --watchedNamespaces=istio-system,default,frontend,backend,database
```

# deploy access log
```bash
istioctl install --set meshConfig.accessLogFile=/dev/stdout
```

# inject envoy
```bash
kubectl label namespace default istio-injection=enabled
kubectl label namespace frontend istio-injection=enabled
kubectl label namespace backend istio-injection=enabled
kubectl label namespace database istio-injection=enabled
kubectl apply -f istio-1.13.3/samples/addons
```

# deploy cert-manager
```bash
helm repo add jetstack https://charts.jetstack.io
```

# update
```bash
helm repo update
```

# deploy cert-manager
```bash
helm install \
 cert-manager jetstack/cert-manager \
 --namespace cert-manager \
 --create-namespace \
 --version v1.8.0 \
 --set installCRDs=true
```

# deploy letsencrypt app.carelyo.in
```bash
kubectl apply -f deployment/istio-app/cert-manager/app.carelyo.in.yaml
```

# staging issuer
```bash
kubectl apply -f deployment/istio-app/cert-manager/staging-cluster.yaml
```

# Secret in namespaces
```bash
kubectl -n frontend create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

kubectl -n backend create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

kubectl -n database create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson
```

# deploy app secrets
```bash
kubectl apply -f deployment/istio-app/secrets/
```

#Proceed? (y/N) 
```bash
y
```

# deploy gateway
```bash
kubectl apply -f deployment/istio-app/login/gateway.yaml
```

# deploy virtualservices
```bash
kubectl apply -f deployment/istio-app/login/virtualservice.yaml
```

# deploy authentication
```bash
kubectl apply -f deployment/istio-app/login/
```

# deploy athourization
```bash
kubectl apply -f deployment/istio-app/login/authorization.yaml
```

#deploy app
```bash
kubectl apply -f deployment/istio-app/login/database.yaml
kubectl apply -f deployment/istio-app/login/login.yaml
kubectl apply -f deployment/istio-app/login/registration-svr.yaml
```