---
sidebar_position: 0
sidebar_label: Setup
---
# Carelyo k8 cluster

## Install OCI CLI
Oracle Cloud infrastructure (OCI) Public Cloud.
This setup requires a linux server. You can use Cloud Shell which is pretty straightforward.
Get the latest OCI CLI version [OCI-CLI](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm#:~:text=Linux%20and%20Unix,Note).
This takes you to **Linux and Unix** where you just follow the guide.

During the installation you will go through the steps described next.

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

## Verify OCI-CLI is installed
To verify that oci was installed type
>
> ```bash
> oci --versio
> ```
> 

## Create a directory to contain the kubeconfig file.
> 
> ```bash
> mkdir -p $HOME/.kube
> ```

## To access the kubeconfig for your cluster
1. Login to OCI 
2. In the search type **OKE**
3. You should see **Service** 
4. Click **Kubernetes Clusters (OKE)**
5. Click the cluster you want to connect to for exmple **ActionClos**
6. Scroll down till you see **Resources** to the left of the sidebar
7. Click **Quick Start**
8. Click **Access cluter**
9. Select **Local Access**
10. Go the section which states **To access the kubeconfig for your cluster via the VCN-Native public endpoint, copy the following command:** and copy the code and past it to your terminal. Follow the below steps:

> ERROR: Could not find config file at /home/ubuntu/.oci/config
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


> Hit enter here
> Enter a location for your config [/home/ubuntu/.oci/config]: 
> 
> 1. Login into your OCI and click your profile icon > User setting
> copy your OCID and paste it here.
> 2. Enter a user OCID:
> 3. Enter a tenancy OCID:
> 4. Enter a region by index or name(e.g.
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
> 5. Do you want to generate a new API Signing RSA key pair? (If you decline you will be asked to supply the path to an existing key.) [Y/n]: Y
>
> 6. Click enter here:
>>Enter a directory for your keys to be created [/home/ubuntu/.oci]:
>> Enter a name for your key [oci_api_key]: 
>> Public key written to: /home/ubuntu/.oci/oci_api_key_public.pem
>> Enter a passphrase for your private key (empty for no passphrase): 
>> Private key written to: /home/ubuntu/.oci/oci_api_key.pem
>> Fingerprint: 79:f9:43:ad:fc:8b:b4:d1:2a:6e:8b:03:53:2a:c5:95
>> Config written to /home/ubuntu/.oci/config
>
>
> 7. If you haven't already uploaded your API Signing public key through the
>    console, follow the instructions on the page linked below in the section
>    'How to upload the public key':
>
>        https://docs.cloud.oracle.com/Content/API/Concepts/apisigningkey.htm#How2
>
>
> 8. Successfully created config file with your new CLI user profile
> Once your public key is uploaded in the console, you can re-run your command to use your new config file and user profile

## Install kubectl
To install [kubctl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).
To set your KUBECONFIG environment variable to the file for this cluster, use:
> 
> ```bash
>  export KUBECONFIG=$HOME/.kube/config
> ```
>
>

## Install ISTIO 
1. Go to [Istio download](https://istio.io/latest/docs/setup/getting-started/#download). It's important to check the link for latest version.
2. Go to the Istio release page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):
   ```bash 
   curl -L https://istio.io/downloadIstio | sh -
   ```
3. Add the istioctl client to your path (Linux or macOS):
   ```bash 
   export PATH="$PATH:/home/admin01/istio-1.13.3/bin" 
   ```
4. Move to the Istio package directory. For example, if the package is istio-1.13.3:
   ```bash 
   cd istio-1.13.3 
   ```
5. Begin the Istio pre-installation check by running:
   ```bash 
   istioctl x precheck
   ```
6. Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:
   ```bash
   kubectl label namespace default istio-injection=enabled
   ```

## ISTIO Useful Commands
1. inspecting the deployments
  ```bash
  kubectl -n istio-system get deploy
  ```
2. You can inspect the installed-state CR, to see what is installed in the cluster, as well as all custom settings.
  ```bash
  kubectl -n istio-system get IstioOperator installed-state -o yaml > installed-state.yaml
  ```
3. Display the names of Istio configuration profiles
  ```bash
  istioctl profile list
  ```
4. View the configuration settings of a *default* profile
   ```bash
   istioctl profile dump default
   ```
5. To view a subset of the entire configuration, you can use the --config-path flag, which selects only the portion of the configuration under the given path.
   ```bash
   istioctl profile dump --config-path components.pilot default
   ```
6. The profile diff sub-command can be used to show the differences between profiles, which is useful for checking the effects of customizations before applying changes to a cluster.
   ```bash
   istioctl profile diff default demo
   ```
7. Execute the following command to determine if your Kubernetes cluster is running in an environment that supports external load balancers:
   ```bash
   kubectl get svc istio-ingressgateway -n istio-system
   ```
8. 
 





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


