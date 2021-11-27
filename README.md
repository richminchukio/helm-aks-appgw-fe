# aks-appgw-fe

publish steps

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

vi Chart.yaml # bump version
helm dep update
helm package .
# helm repo index . --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
rm -r charts/
helm repo index . --merge index.yaml --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
# fix tar.gz
helm dep update
git add *
git commit -m ""
git tag aks-appgw-fe-$(yq eval '.version' Chart.yaml)
git push --all
git push --tags
helm repo update
```