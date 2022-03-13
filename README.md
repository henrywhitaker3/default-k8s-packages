# ArgoCD Defaults

## Install

First install ArgoCD itself:

```shell
kubectl create namespace argocd
helm install -n argocd -f argo-cd/values.yaml argocd argo-cd/
```

Then install the root app (which includes argo) so that any apps added to a values file automatically get picked up by argo from here:

```shell
helm -n argocd -f apps/values.yaml template apps | kubectl apply -f -
```

Remove helm ownership of argo:

```shell
kubectl -n argocd delete secret -l owner=helm,name=argocd
```