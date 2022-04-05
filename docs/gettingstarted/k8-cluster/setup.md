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

## Create Secrets 
> 1. Create a secret for docker login:
> 
> ```bash
>   kubectl -n carelyo-stage create secret swecon-dh \
>   --from-file=.dockerconfigjson=home/admin/.docker/config.json \
>   --type=kubernetes.io/dockerconfigjson
> ```
> 2. For example: To Creat a secret for mailuser
> ```bash
    kubectl create secret generic mail-username --type=string --from-literal=MAIL_USERNAME=donotreply@carelyo.ng
  ```
> 
> View all secrets
> 
> ```bash
> kubectl get secrets
> ```

>## Install ingress Contoller. This command also upgrades the ingress controller as well
>``` bash
>  helm upgrade --install ingress-nginx ingress-nginx \
>  --repo https://kubernetes.github.io/ingress-nginx \
>  --namespace ingress --create-namespace
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
> 
> ```bash
> kubectl get pods
> kubectl logs "podaname" --follow
> kubectl describe svc "servicename"
> kubectl get ing "ingressResourceName"
> kubectl get ns
