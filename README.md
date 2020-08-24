# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## bootstrapping
1. Initialize create argo:
```
kubectl create namespace argocd
kubectl config set-context --current --namespace=argocd
```

2. Login via the CLI (pwd is the name of the `argo-server`):
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
argocd login localhost:8080
```

3. Bootstrap the main application:
```
argocd app create main \
--dest-namespace argocd \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/entropy-fund/deploy-dev.git \
--path main
```

4. Set main to autosync:
```
argocd app set main --sync-policy automated
argocd app set main --auto-prune
```

5. Add a DNS record (using the IP of the ingress-nginx and the host in `argocd/ingress.yaml`)
