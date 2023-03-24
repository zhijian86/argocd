# argocd

installation

You need to create a namespace for argocd.

```bash
kubectl create ns argocd
```

<details>
<summary>and then choose one of the below options :<summary>

1. Non-HA:

a. cluster-admin privileges: https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

b. namespace level privileges: https://github.com/argoproj/argo-cd/raw/stable/manifests/namespace-install.yaml

2. HA:

a. cluster-admin privileges: https://github.com/argoproj/argo-cd/raw/stable/manifests/ha/install.yaml

b. namespace level privileges: https://github.com/argoproj/argo-cd/raw/stable/manifests/ha/namespace-install.yaml

3. Light installation "Core"

https://github.com/argoproj/argo-cd/raw/stable/manifests/core-install.yaml

4. Helm chart: https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd

</details>

removing argocd

```bash
kubectl delete -f nonha_installation.yaml
```

get all namespace

```bash
kubectl get ns
```

switch namespace

```
kubectl config set-context --current --namespace=argocd
```

add argocd, make sure you are on the right ns

```
kubectl create -f nonha_installation.yaml
```
