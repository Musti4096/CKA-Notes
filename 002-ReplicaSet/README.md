# Kubernetes CLI ReplicaSet commands

## ReplicaSet

- Create replicaSets

```bash
kubectl apply -f replicaset.yml
```

- Inspect the replicasets

```bash
kubectl describe rs newreplicaset
kubectl get rs -o wide
```

-Delete replicasets

```bash
kubectl delete rs newreplicaset
```
