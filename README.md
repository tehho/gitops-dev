# gitops-dev
Declarative spec for the dev cluster on GCP managed by ArgoCD

## bootstrapping
1. Initialize create argo:
```
cd main
kubectl apply -k .
```

2. Add a DNS record (using the IP of the ingress-nginx and the host in `argocd/ingress.yaml`)

3. Login via the CLI (pwd is the name of the `argo-server`):
```
argocd login <Server DNS>
argocd account update-password
```

4. 
