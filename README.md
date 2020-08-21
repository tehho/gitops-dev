# deploy-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## setup

1. `kubectl create namespace nginx-ingress`
2. `kubectl config set-context --current --namespace=nginx-ingress`
3. `helm install nginx-ingress ingress-nginx/ingress-nginx  --set controller.extraArgs.enable-ssl-passthrough=true`
4. Get ingress IP with `kubectl get ingress` and add DNS record.
5. `kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.1/cert-manager.yaml`
6. `kubectl apply -f setup/clusterissuer.yaml`
7. 

## global
Cert manager is installed (for https) globally:
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.1/cert-manager.yaml
```
and additional resources in `/global`

## nginx-ingess ns
Nginx is installed as ingress:
```
kubectl config set-context --current --namespace=nginx-ingress
```

## argocd ns

