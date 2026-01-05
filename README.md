# Argo-CD
This repo has manifests and procedure to installation of agro-cd &amp; basic to advanced argo usecases



## Prerequisites
- Kubernetes cluster (v1.32+)
- kubectl CLI installed and configured
- argocd CLI installed
- Helm CLI installed (optional, for Helm charts)
- Git installed
- Access to a Git repository (e.g., GitHub, GitLab)


### Creating the argo application through application.yaml
```
    kubectl create namespace rotiva-Labs-app
    kubectl apply -f rotiva-labs-sample/application.yaml -n rotiva-Labs-app
```

```
    argocd app sync rotiva-labs-app
```

### Creating the argo application through argo-cli
```
    argocd app create rotiva-Labs-app \
    --repo https://github.com/shashi0396/Argo-CD.git \
    --revision master \
    --path rotiva-labs-sample \
    --dest-server https://kubernetes.default.svc \
    --dest-namespace rotiva-Labs-app \
    --project default \
    --sync-option CreateNamespace=true
    # --argo-namespace cd-tools  # if argo installed elsewhere otherthan argo-cd namespace

```

```
    argocd app sync rotiva-labs-app
```

### List all argo applications

```
    argocd app list
    argocd app get rotiva-labs-app
```

### Tool NOT Set , Auto-Detected by Argo

Even if NOT explicitly set , Argo detects the tool as follows:
- **Helm charts:** if there is a file as chart.yaml
- **kustomize:** if there's a kustomization.yaml or Kustomization
otherwise it's assumed as plain Yaml **directory** application