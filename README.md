# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## setup

1. `kubectl create namespace nginx-ingress`
2. `kubectl config set-context --current --namespace=nginx-ingress`
3. `helm install nginx-ingress ingress-nginx/ingress-nginx  --set controller.extraArgs.enable-ssl-passthrough=true`
4. Get ingress IP with `kubectl get ingress` and add DNS record.
5. `kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.1/cert-manager.yaml`
6. `kubectl apply -f bootstrap/clusterissuer.yaml`
7. `kubectl create namespace argocd`
8. `kubectl config set-context --current --namespace=argocd`
9. `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
10. 
```
argocd app create main \
--dest-namespace argocd \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/entropy-fund/deploy-dev.git \
--path argocd
```


