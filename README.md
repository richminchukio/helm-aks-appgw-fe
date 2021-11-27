# aks-appgw-fe

publish steps

```sh
vi Chart.yaml # bump version
git add *
git commit -m ""
git tag aks-appgw-fe-$(yq eval '.version' Chart.yaml)
git push --follow-tags
helm package .
helm repo index . --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
helm repo index . --merge index.yaml --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
sed 
```