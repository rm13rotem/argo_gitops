# argo_gitops
a git repository for handling the argocd


# Lab 1 - create project:

1. Create git repo named gitops
2. Create new project in argocd and connect it to your gitops repo

## Example project yaml 

```
apiVersion: argoproj.io/v1alpha1
kind: AppProject
metadata:
  name: my-project
  namespace: argocd
spec:
  description: Allow access to a specific Git repository and branch
  sourceRepos:
    - https://github.com/rm13rotem/argo-gitops.git
  destinations:
    - namespace: '*'
      server: https://kubernetes.default.svc
  sourceNamespaces:
    - '*'
```





# Lab 2  - create Application:


Create new application using Yaml
Example


```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: demo-app
  namespace: argocd
spec:
  project: my-project
  source:
    repoURL: https://github.com/rm13rotem/argo-gitops.git
    path: .
  destination:
    server: https://kubernetes.default.svc
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true

```




# Lab 3 - using Helm

1. Use this example yaml:
https://github.com/elevy99927/Jenkins-k8s/blob/main/Part4-CICD/04-ArgoCD/yamls/demo-app.yaml
2. Task 1: Create application in ArgoCD using the Application CRD.

 source:
    repoURL: https://stefanprodan.github.io/podinfo
    chart: podinfo
    targetRevision: 6.5.0

