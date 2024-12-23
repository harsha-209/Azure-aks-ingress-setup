# Azure-aks-ingress-setup
follow aks doucmentation for nginx ingress in aks cluster 

https://learn.microsoft.com/en-us/troubleshoot/azure/azure-kubernetes/load-bal-ingress-c/create-unmanaged-ingress-controller?tabs=azure-cli


let's install nginx ingress on aks cluster by following below document

1. helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx
2. it will create a loadbalaner ip in aks cloud
3. deploy you application **#NOTE** **DEPLOY THE APPLICATION IN SAME NAMESPACE ,WHERE INGRESS CONTROLLER INSTALLED/SETUP**(IF NOT, YOU MAY FACE NOT REACHABLE ISSUE)
4. now deploy ingresswithoutssl yaml file
5. now you can access the app with nginx ingress ip

# install certificate manager to setup nginx ingress with ssl

   1. helm repo add jetstack https://charts.jetstack.io --force-update
   2. helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.16.2 \
  --set crds.enabled=true
3. now deploy the issue-certificate yaml file
4. after above successfully deployment, now you can deploy ingress with ssl successfully
5. wait for sometime around 15mins, and acces the web

   ingress setup link: https://ammarsuhail155.medium.com/ingress-controller-nginx-deployment-on-azure-kubernetes-services-29ca0a668083
   certificate manger link: https://cert-manager.io/docs/tutorials/getting-started-aks-letsencrypt/


# setup the azure key vault to access from aks pod application
   
first you have to export below vairable as environment variables
enable csi drive installation in while aks creation setup time

export RESOURCE_GROUP=Notify
export UAMI=aks-keyvault2 ###name of the managed identity created
export KEYVAULT_NAME=aks-keyvaut
export CLUSTER_NAME=harshad

1. create a managed identiy
2. map the above managed identiy to azurekey vault servie, which you created and assign key vault admistration role to it
3. before the you have enable to oidc issue for aks cluster
follow the abhishekverramall document azure zero to hero 
