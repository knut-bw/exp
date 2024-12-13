[Complete]
1. 安裝alloy & beyla

[Pending]
1. 安裝 jaeger & grafana & tempo
2. 隨便找個微服務串接資料

# install helm
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

# install alloy
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
kubectl create namespace fcts
kubectl delete namespaces fcts
kubectl create namespace exp
helm install --namespace exp alloy grafana/alloy
kubectl get pods --namespace exp

# apply beyla(don't install controller)
kubectl apply -f beyla_sc.yaml
kubectl apply -f beyla.yaml
