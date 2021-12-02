# richminchukio/aks-appgw-fe helm chart deploy notes

Due to [existing deficiencies in dependent charts](https://github.com/jetstack/cert-manager/issues/4613#issuecomment-982906448) you must first manually apply Cert-Manager CRDs.

```sh
# because.. reasons
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.6.1/cert-manager.crds.yaml

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