# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## bootstrapping
1. Initialize create argo:
```
kubectl create namespace argocd
kubectl config set-context --current --namespace=argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl apply -f argocd/ingress.yaml
```

2. Add a DNS record (using the IP in `kubectl get ingress` and the host in `argocd/ingress.yaml`) an then login via the CLI:
```
argocd login <ARGOCD_SERVER>
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
