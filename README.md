# richminchukio/aks-appgw-fe helm chart

## WHAT IS IT?

Azure Kubernetes Service + Azure Application Gateway + Azure Active Directory Pod Identity + Azure Ingress Controller + JetStack Cert-Manager Let's Encrypt + frontend httpd container deployment. Or otherwise: terminate SSL at Azure Application Gateway and direct traffic to a front end container living in Azure Kubernetes Service. 

This software is provided ["AS IS," WITHOUT WARRANTY OF ANY KIND...](./LICENSE.txt)

The recommended way to deploy this chart is to use the [aks_appgw_fe terraform registry module](https://registry.terraform.io/modules/richminchukio/aks-appgw-fe/azurerm/latest).

---

### MANUAL CHART INSTALL

Due to [existing deficiencies in dependent charts](https://github.com/jetstack/cert-manager/issues/4613#issuecomment-982906448) you must first manually apply Cert-Manager CRDs to use the `aks_appgw_fe` chart.

```sh
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.6.1/cert-manager.crds.yaml

helm repo add richminchukio https://raw.githubusercontent.com/richminchukio/helm-aks-appgw-fe/main/
helm install httpd-chart richminchukio/aks_appgw_fe \
  --version=1.0.0 \
  --set issuer.enabled=true \
  --set ingress.host=************** \
  --set aadpodidbinding=aad-pod-identity \
  --set aks-appgw-fe.ingress-azure.appgw.subscriptionId=************** \
  --set aks-appgw-fe.ingress-azure.appgw.resourceGroup=************** \
  --set aks-appgw-fe.ingress-azure.appgw.name=************** \
  --set aks-appgw-fe.ingress-azure.appgw.usePrivateIP=false \
  --set aks-appgw-fe.ingress-azure.appgw.shared=false \
  --set aks-appgw-fe.ingress-azure.armAuth.type=aadPodIdentity \
  --set aks-appgw-fe.ingress-azure.armAuth.identityResourceID=************** \
  --set aks-appgw-fe.ingress-azure.armAuth.identityClientID=************** \
  --set aks-appgw-fe.ingress-azure.rbac.enabled=true \
  --set aks-appgw-fe.cert-manager.installCRDS=false \
  --set aks-appgw-fe.cert-manager.startupapicheck.enabled=false
```