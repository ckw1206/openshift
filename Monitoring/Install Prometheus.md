### Install Helm
```
sudo apt install helm
```
### Add Prometheus Community Helm repo
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
### Update Helm
```
helm repo update
```
### Install Prometheus in default
```
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
```
### Port forwarding
```
kubectl port-forward -n=monitoring svc/kube-prometheus-stack-grafana 8080:80
```
