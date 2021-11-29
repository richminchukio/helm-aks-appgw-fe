# aks-appgw-fe

deploy notes

```sh
helm install httpd-chart ./ \
  --set issuer.aksappgwfe.enabled=false \
  --set ingress.aksappgwfe.host=************** \
  --set aadpodidbinding=************** \
  --set ingress-azure.appgw.subscriptionId=************** \
  --set ingress-azure.appgw.resourceGroup=************** \
  --set ingress-azure.appgw.name=************** \
  --set ingress-azure.appgw.usePrivateIP=false \
  --set ingress-azure.appgw.shared=false \
  --set ingress-azure.armAuth.type=aadPodIdentity \
  --set ingress-azure.armAuth.identityResourceID************** \
  --set ingress-azure.armAuth.identityClientID=************** \
  --set ingress-azure.rbac.enabled=true \
  --set cert-manager.installCRDS=true \
  --set cert-manager.startupapicheck.enabled=false
```