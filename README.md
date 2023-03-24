### argocd

## installation

You need to create a namespace for argocd.

```bash
kubectl create ns argocd
```

<details>
<summary>and then choose one of the below options :</summary>

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

```bash
kubectl config set-context --current --namespace=argocd
```

verify you are in the correct ns

```bash
kubectl config get-contexts
```

add argocd, make sure you are on the right ns

```bash
kubectl create -f nonha_installation.yaml
```

ArgoCD inital pw

```bash
kubectl get secret
kubectl get secret argocd-initial-admin-secret -o yaml
```

convert password from base64string - dYLBXTlexf1JQ-Nm

```bash
 [Text.Encoding]::Utf8.GetString([Convert]::FromBase64String('ZFlMQlhUbGV4ZjFKUS1ObQ=='))
```

<details>
<summary>3 ways to expose argocd cluster</summary>
1. You can change the argocd server service type into load balancer if you are using a managed Kubernetes service in a cloud like AWS or Azure or GCP.  
2. Use Ingress resources to point to the server
3. Port forwarding (for local instances)
```bash
kubectl port-forward svc/argocd-server 8080:443
```
https://localhost:8080/login?return_url=https%3A%2F%2Flocalhost%3A8080%2Fapplications
</details>

## installing ArgoCD CLI

https://argo-cd.readthedocs.io/en/stable/cli_installation/

```bash
$version = (Invoke-RestMethod https://api.github.com/repos/argoproj/argo-cd/releases/latest).tag_name
```

```bash
$url = "https://github.com/argoproj/argo-cd/releases/download/v2.6.7/argocd-windows-amd64.exe"
$output = "argocd.exe"

Invoke-WebRequest -Uri $url -OutFile $output
```

set the exe path in environment variable
run command

```bash
argocd version
```

login to argocd CLI

```bash
argocd login localhost:8080
```

cluster list via cli

```bash
argocd cluster list
```

## Creating Application

contains destination(target cluster/namespace) and source(desired state in git repo/revision/path)
There are 3 ways to create application namely through yaml, UI or cli

```bash
kubectl create -f application.yaml
```
