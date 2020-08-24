# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## bootstrapping

```
argocd app create main \
--dest-namespace argocd \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/entropy-fund/deploy-dev.git \
--path main
--sync-policy automated
--auto-prune
```


