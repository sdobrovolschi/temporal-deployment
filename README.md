### Recovering From an Existing Repository
To recover the Argo CD installation run:
```bash
export GIT_REPO=<REPO_URL>
export GIT_TOKEN=<YOUR_TOKEN>

argocd-autopilot repo bootstrap --recover
```


### Apply Argo-CD Manifests From Existing Repository
To apply the modified Argo CD manifests run:
```bash
export GIT_REPO=<REPO_URL>
export GIT_TOKEN=<YOUR_TOKEN>

argocd-autopilot repo bootstrap --recover --app "${GIT_REPO}.git/bootstrap/argo-cd"
```

### Argo CD Browsing
To browse Argo CD to `http://localhost:8080` run:
```bash
kubectl port-forward -n argocd svc/argocd-server 8080:80
```

### Temporal FrontEnd Exposure
To expose Temporal FrontEnd to `http://localhost:7233` run:
```bash
kubectl port-forward -n temporal svc/temporal-frontend-headless 7233:7233
```

### Temporal Web UI Browsing
To browse Temporal Web UI to `http://localhost:9090` run:
```bash
kubectl port-forward -n temporal svc/temporal-we 9090:8080
```
