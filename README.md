# aks-appgw-fe

deploy notes

```sh
helm install httpd-chart ./ \
  --set issuer.enabled=true \
  --set ingress.host=************** \
  --set aadpodidbinding=************** \
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