# argocd
Tutorial how to start argocd


# How to get password for argo UI

Username: admin  
You can check the password from this command:  
``` kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d ```
