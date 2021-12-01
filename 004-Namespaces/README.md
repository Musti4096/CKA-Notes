# Kubernetes CLI commands

## Namespaces

- how can we call any service from another name space

```bash
mysql.connect("db-service.dev.svc.cluster.local)
```

- List pods on specific Namespace

```bash
kubectl get pods --namespace=kube-system
```

- Create a pod on specific Namespace (you can also add namespace on yml file)

```bash
kubectl create -f pod-definition.yml --namespace=dev
```

- Create a namespace

```bash
kubectl create -f namaspace-dev.yml
or
kubectl create namespace dev
```

- Switch namespace

```bash
kubectl config set-context $(kubectl config current context) --namespace=dev
kubectl config set-context $(kubectl config current context) --namespace=prod
kubectl config set-context $(kubectl config current context) --namespace=default
```

- Get pods from all namespaces

```bash
kubectl get pods --all-namespaces
```

- Define quota for namespaces

```bash
kubectl create -f compute-quota.yml
```
