# 3scale App of Apps

Para instanciar todas as Applications, AppProjects e etc. Presentes neste repositório crie a seguinte Application no ArgoCD, ele atuará como bootstrap para instanciar tudo que está em GitOps relacionado ao 3scale:

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: 3scale-app-of-apps
  namespace: openshift-gitops
  labels:
    3scale: gitops
spec:
  destination:
    name: in-cluster
    namespace: ''
    server: ''
  source:
    path: .
    repoURL: 'https://github.com/adregis/gitops-3scale-app-of-app.git'
    targetRevision: HEAD
    directory:
      recurse: true
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - Replace=true
      - ApplyOutOfSyncOnly=true
```
