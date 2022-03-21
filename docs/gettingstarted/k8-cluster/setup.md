---
sidebar_position: 1
sidebar_label: Setup
---
# Carelyo k8 cluster

> Setup k8 cluster

## Login to OCI
> - Login to OCI and in the search type OKE
> - Click create cluster
> - Give the cluster a name carelyo-cluster
> - Remember to add ssh key
> - Leave all default and click next and then create.
> - Done!

## Connect to Cluster Cloud shell
> - Search oke 
> - Click the cluster carelyo-cluster
> - Scroll down and at the left click Quick Start
> - Click Access Cluster
> - - Click Launch Cloud Shell
> - - To access the kubeconfig for your cluster via the VCN-Native public endpoint, copy the following command:
> - -  Close.

## Create a certificate manager for the cluster
> ```bash
> kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.7.1/cert-manager.yaml
> ```
> 
> To see the Cert-manager
>```bash
> kubectl -n cert-manager get all
>```

## Install Haproxy Ingress controller
> - From Cloud shell get the helm repo for haproxy ingress controller

>```bash
> helm repo add haproxy-ingress https://haproxy-ingress.github.io/charts
>```
> - Create a file haproxy-ingress-values.yaml and add this content into it.

> ```bash
> controller:
>  hostNetwork: true
>  ```

> - Install the haproxy ingress controller withh this command
> ```bash
> helm install haproxy-ingress haproxy-ingress/haproxy-ingress\
>  --create-namespace --namespace ingress-controller\
>  --version 0.13.6\
>  -f haproxy-ingress-values.yaml
> ```
> [Haproxy Ingress Controller] ![https://haproxy-ingress.github.io/docs/getting-started/]
> 
## Create Cert Issuers
>
> View the clusterissuers
> ```bash
> kubectl get clusterissuer
> ```

## Create Secrets 
> 1. Create a secret for docker login:
> 
> ```bash
> kubectl -n carelyo-stage create secret swecon-dh \
>   --from-file=.dockerconfigjson=home/admin/.docker/config.json \
>   --type=kubernetes.io/dockerconfigjson
> ```
> 
> View all secrets
> 
> ```bash
> kubectl get secrets
> ```

## To deploy login deployment and service
> In the deployment > k8 > login folder 
> - Modify and then apply the deployment yaml file
> - This file has two sections:
> - - login deployment
> - - login service
> - Apply it into the carelyo-stage namespace
> ```bash
> kubectl apply -f deploy_login.yaml -n carelyo-stage
> ```

## To deploy login Ingress
> In the deployment > k8 > login folder
> - Create a new file for the login ingress deployment
> - Apply it into the the carelyo-stage namespace
> ```bash
> kubectl apply -f haproxy-login-ingress.yaml -n carelyo-stage
> ```