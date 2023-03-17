# argocd
Tutorial how to start argocd


# How to get password Argo UI

Username: admin  
You can check the password from this command:  
``` kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d ```

## kustomize

```kubectl apply -k .```

```cd /dev/```
```kustomize build . | kubectl apply -f - ```


## Kustimize with ArgoCD

ArgoCD have native support of kustomize.

```


apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: bgdk-app
  namespace: argocd
spec:
  destination:
    namespace: bgdk
    server: https://kubernetes.default.svc
  project: default
  source:
    path: apps/bgd/overlays/bgdk
    repoURL: https://github.com/redhat-developer-demos/openshift-gitops-examples
    targetRevision: minikube
  syncPolicy:
    automated:
      prune: true
      selfHeal: false
    syncOptions:
    - CreateNamespace=true
```

## Using helm

### Install helm3

```curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash```

### Setup repo

```
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo list
```

Try install wordpress:
```
helm search repo wordpress

helm install blog  stable/wordpress

kubectl get all -l "release=blog"
```
