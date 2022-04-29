---
sidebar_position: 0
sidebar_label: Istio-Script
---
# Istio Installation Script

### Istio Install Script

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
### Export the path
```bash
export PATH="$PATH:/home/admin01/istio-1.13.3/bin"
```
 or 

```bash
cd istio-1.13.3
sudo cp bin/istiocli /usr/local/bin/istiocli
```


### validate
```bash
istioctl x precheck
```

### insall istio
```bash
istioctl install
```

### when you see Proceed? (y/N)
```bash 
y
```

### Install istio operator which automate updates etc. of istio 
```bash
istioctl operator init --watchedNamespaces=istio-system,default,frontend,backend,database
```

### deploy access log
```bash
istioctl install --set meshConfig.accessLogFile=/dev/stdout
```

### inject envoy
```bash
kubectl label namespace default istio-injection=enabled
kubectl label namespace frontend istio-injection=enabled
kubectl label namespace backend istio-injection=enabled
kubectl label namespace database istio-injection=enabled
kubectl apply -f istio-1.13.3/samples/addons
```

### deploy cert-manager
```bash
helm repo add jetstack https://charts.jetstack.io
```

### update
```bash
helm repo update
```

### deploy cert-manager
```bash
helm install \
 cert-manager jetstack/cert-manager \
 --namespace cert-manager \
 --create-namespace \
 --version v1.8.0 \
 --set installCRDs=true
```

### deploy letsencrypt app.carelyo.in
```bash
kubectl apply -f deployment/istio-app/cert-manager/app.carelyo.in.yaml
```

### staging issuer
```bash
kubectl apply -f deployment/istio-app/cert-manager/staging-cluster.yaml
```

### Secret in namespaces
```bash
kubectl -n default create secret generic swecon-dh \
--from-file=.dockerconfigjson=/home/deploy/.docker/config.json \
--type=kubernetes.io/dockerconfigjson

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

### deploy app secrets
```bash
kubectl apply -f deployment/istio-app/secrets/
```

### Proceed? (y/N) 
```bash
y
```

### deploy gateway
```bash
kubectl apply -f deployment/istio-app/login/gateway.yaml
```

### deploy virtualservices
```bash
kubectl apply -f deployment/istio-app/login/virtualservice.yaml
```

### deploy authentication
```bash
kubectl apply -f deployment/istio-app/login/
```

### deploy athourization
```bash
kubectl apply -f deployment/istio-app/login/authorization.yaml
```

### deploy app
```bash
kubectl apply -f deployment/istio-app/login/database.yaml
kubectl apply -f deployment/istio-app/login/login.yaml
kubectl apply -f deployment/istio-app/login/registration-svr.yaml
```
### Point dns for the app-carelyo.in. First to get the loadbalancer ip, copy run.
```bash
kubectl apply -f deployment/istio-app/login/
```
### The result show the istio-ingressgateway. Copy the External IP 130.162.53.180
```bash
NAME                        TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                                      AGE
cm-acme-http-solver-cgx6q   NodePort       10.96.197.69    <none>           8089:31892/TCP                               12m
grafana                     ClusterIP      10.96.119.53    <none>           3000/TCP                                     16m
istio-ingressgateway        LoadBalancer   10.96.65.24     130.162.53.180   15021:31203/TCP,80:32045/TCP,443:30191/TCP   25m
istiod                      ClusterIP      10.96.214.12    <none>           15010/TCP,15012/TCP,443/TCP,15014/TCP        26m
jaeger-collector            ClusterIP      10.96.110.154   <none>           14268/TCP,14250/TCP,9411/TCP                 16m
kiali                       ClusterIP      10.96.108.115   <none>           20001/TCP,9090/TCP                           16m
```

### In OCI type zone in the search
1. Select the develop compartment and you will see carelyo.in
2. Click carelyo.in
3. Scroll down and to the left you should see Resources
4. Click Records
5. Click Add Record if the record doesn't exist. If it does edit it. Add an A Record which maps to this 130.162.53.180. 
6. Finally, click Publish

### Chet thet the application is running for example the login 
```bash
kubectl exec "$(kubectl get pod -l app=login -o jsonpath='{.items[0].metadata.name}')" -c login -- curl -sS login:80 | grep -o "<title>.*</title>"
<title>Carelyo</title>
```

