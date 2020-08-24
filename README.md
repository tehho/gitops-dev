# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## bootstrapping
1. Initialize namespace:
```
cd main
kubectl apply -k .
```

2. Start ArgoCD:
```
kubectl config set-context --current --namespace=argocd
cd ../argocd
kubectl apply -k .
```

3. Login via the CLI on localhost (pwd is the name of the `argo-server`):
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
argocd login localhost:8080
argocd account update-password
```

4. Start the main application:
```
argocd app create main \
--dest-namespace argocd \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/entropy-fund/deploy-dev.git \
--path main
```

5. Set main application to autosync:
```
argocd app set main --sync-policy automated
argocd app set main --auto-prune
```

6. Add a DNS record (using the IP of the ingress-nginx and the host in `argocd/ingress.yaml`)

7. Login via the CLI (or via web app):
```
argocd login <Server DNS>
```
