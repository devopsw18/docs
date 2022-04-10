---
sidebar_position: 0
sidebar_label: Setup
---
# Carelyo k8 cluster

## Setup your local machine to connect with OKE CLuster running on OCI (Oracle Cloud Infrastructure Console) for Linux [See here for Windows/Mac](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm)

> ```bash
> bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
> ```
>
>Hit enter when you see this
>
> ```bash
> ===> In what directory would you like to place the install? (leave blank to use '/home/ubuntu/lib/oracle-cli'):
> ===> In what directory would you like to place the 'oci' executable? (leave blank to use '/home/ubuntu/bin'):
> ===> In what directory would you like to place the OCI scripts? (leave blank to use '/home/ubuntu/bin/oci-cli-scripts'):
> ==> Currently supported optional packages are: ['db (will install cx_Oracle)']
> What optional CLI packages would you like to be installed (comma separated names; press enter if you don't need any optional packages)?:
>
> At this point you will be asked to enter your linux password
> 
> -- The optional packages installed will be ''.
> -- Executing: ['sudo', 'apt-get', 'update']
> [sudo] password for ubuntu: *********     
>
> Enter Y
> 
> ===> Modify profile to update your $PATH and enable shell/tab completion now? (Y/n): Y
>
> Hit Enter
> 
> ===> Enter a path to an rc file to update (file will be created if it does not exist) (leave blank to use '/home/ubuntu/.bashrc'):
>
> To verify that oci was installed type
> 
> oci --versio
> 
> ```
> 1. Create a directory to contain the kubeconfig file.
> 
> ```bash
> mkdir -p $HOME/.kube
> ```
> 2. To access the kubeconfig for your cluster via the VCN-Native public endpoint, copy the following command:
> 
> ```bash
> oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.eu-frankfurt-1.aaaaaaaa2gq2cpd27cclfcyszr2dwlo77ezgob4txjeaaqqbzcej7mdomroa --file $HOME/.kube/config --region eu-frankfurt-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
ERROR: Could not find config file at /home/ubuntu/.oci/config
> Do you want to create a new config file? [Y/n]: y
> Do you want to create your config file by logging in through a browser? [Y/n]: n
>    This command provides a walkthrough of creating a valid CLI config file.
>
>    The following links explain where to find the information required by this
>    script:
>
>    User API Signing Key, OCID and Tenancy OCID:
>
>        https://docs.cloud.oracle.com/Content/API/Concepts/apisigningkey.htm#Other
>
>    Region:
>
>        https://docs.cloud.oracle.com/Content/General/Concepts/regions.htm
>
>    General config documentation:
>
>        https://docs.cloud.oracle.com/Content/API/Concepts/sdkconfig.htm
>
> Hit enter here
> Enter a location for your config [/home/ubuntu/.oci/config]: 
> 
> Login into your OCI and click your profile icon > User setting
> copy your OCID and paste it here.
> Enter a user OCID:
> Enter a tenancy OCID:
> Enter a region by index or name(e.g.
> 1: af-johannesburg-1, 2: ap-chiyoda-1, 3: ap-chuncheon-1, 4: ap-dcc-canberra-1, 5: ap-hyderabad-1,
> 6: ap-ibaraki-1, 7: ap-melbourne-1, 8: ap-mumbai-1, 9: ap-osaka-1, 10: ap-seoul-1,
> 11: ap-singapore-1, 12: ap-sydney-1, 13: ap-tokyo-1, 14: ca-montreal-1, 15: ca-toronto-1,
> 16: eu-amsterdam-1, 17: eu-frankfurt-1, 18: eu-marseille-1, 19: eu-milan-1, 20: eu-stockholm-1,
> 21: eu-zurich-1, 22: il-jerusalem-1, 23: me-abudhabi-1, 24: me-dcc-muscat-1, 25: me-dubai-1,
> 26: me-jeddah-1, 27: sa-santiago-1, 28: sa-saopaulo-1, 29: sa-vinhedo-1, 30: uk-cardiff-1,
> 31: uk-gov-cardiff-1, 32: uk-gov-london-1, 33: uk-london-1, 34: us-ashburn-1, 35: us-gov-ashburn-1,
> 36: us-gov-chicago-1, 37: us-gov-phoenix-1, 38: us-langley-1, 39: us-luke-1, 40: us-phoenix-1,
> 41: us-sanjose-1): 17
> 
> Do you want to generate a new API Signing RSA key pair? (If you decline you will be asked to supply the path to an existing key.) [Y/n]: Y
> 
> click enter here
> Enter a directory for your keys to be created [/home/ubuntu/.oci]:
> Enter a name for your key [oci_api_key]: 
> Public key written to: /home/ubuntu/.oci/oci_api_key_public.pem
> Enter a passphrase for your private key (empty for no passphrase): 
> Private key written to: /home/ubuntu/.oci/oci_api_key.pem
> Fingerprint: 79:f9:43:ad:fc:8b:b4:d1:2a:6e:8b:03:53:2a:c5:95
> Config written to /home/ubuntu/.oci/config
>
>
>    If you haven't already uploaded your API Signing public key through the
>    console, follow the instructions on the page linked below in the section
>    'How to upload the public key':
>
>        https://docs.cloud.oracle.com/Content/API/Concepts/apisigningkey.htm#How2
>
>
> Successfully created config file with your new CLI user profile
> Once your public key is uploaded in the console, you can re-run your command to use your new config file and user profile


> You need to install [kubctl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
>


>
>
> 3. To set your KUBECONFIG environment variable to the file for this cluster, use:
> 
> ```bash
>  export KUBECONFIG=$HOME/.kube/config
> ```
>
>

# Setup a k8 cluster

## Login to OCI
> - Login to OCI and in the search type OKE
> - Click create cluster from OCI Console 
> - Give the cluster a name carelyo-cluster
> - Remember to add ssh key
> - Leave all default and click next and then create.
> - Done!

## Connect to Cluster Cloud shell
> - Search oke 
> - Click the cluster carelyo-cluster
> - Scroll down and at the left click Quick Start
> - Click Access Cluster
> - - Click Launch Cloud Shell or Local Access (for Local Access you must have doing the first step)
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

## To see which Kubernetes resources are and aren't in a namespace:
> ```bash
> # In a namespace
> kubectl api-resources --namespaced=true

> # Not in a namespace
> kubectl api-resources --namespaced=false


> kubectl get pods
> kubectl get pods -l 'environment in (production, qa)'
> kubectl logs "podaname" --follow
> kubectl describe svc "servicename"
> kubectl get ing "ingressResourceName"
> kubectl get ns
> ```


