# helm
 Setting up Helm on your machine. This will allow you to deploy tiller to a namespace called `airwave-tiller`
 while allowing you to deploy to a namespace called `airwave-deploy`.

## RBAC Setup
### tiller service account as Cluster Admin
```
kubectl apply -f rbac-clusterrole.yml
helm init --service-account tiller --history-max 200
```

### tiller service account in its own namespace
```
kubectl apply -f airwave-tiller-ns.json
kubectl apply -f airwave-deploy-ns.json
kubectl apply -f airwave-tiller-role.yml
kubectl apply -f rbac-deploy-role.yml
helm init --service-account tiller --tiller-namespace airwave-tiller --history-max 200
```

## Install a chart to a specific namespace
```
helm install stable/mysql --namespace airwave-tiller --tiller-namespace airwave-tiller
```