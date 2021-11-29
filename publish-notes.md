```sh
vi Chart.yaml # bump version
helm dep update
rm aks-appgw-fe-*.tgz
helm package .
# helm repo index . --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
rm -r charts/
helm repo index . --merge index.yaml --url https://github.com/richminchukio/helm-aks-appgw-fe/archive/refs/tags/
# fix tar.gz
rm aks-appgw-fe-*.tgz
helm dep update
vi CHANGELOG.md
git add *
git commit -m ""
git tag aks-appgw-fe-$(yq eval '.version' Chart.yaml)
git push --all
git push --tags
helm repo update
```