Here is the yaml to create an Argo CD Application for guestbook.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: guestbook
  namespace: argocd
spec:
  destination:
    server: https://kubernetes.default.svc
  project: default
  source:
    path: kubernetes/guestbook/manifests
    repoURL: https://github.com/edge-experiments/gitops-source.git
    targetRevision: main
  syncPolicy:
    automated: {}
```

Here is the yaml to create an Argo CD Application for nginx.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: nginx
  namespace: argocd
spec:
  destination:
    server: https://kubernetes.default.svc
  project: default
  source:
    path: kubernetes/nginx/manifests
    repoURL: https://github.com/edge-experiments/gitops-source.git
    targetRevision: main
  syncPolicy:
    automated: {}
```
