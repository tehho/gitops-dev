# infra-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

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

