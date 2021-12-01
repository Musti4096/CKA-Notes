# Kubectl Advanced Commands

- Get the info in Json format

```bash
kubectl get nodes -o json

kubectl get pods -o json
```

- JsonPath Query

```bash
.items[0].spec.containers[0].image

kubectl get pods -o=jsonpath='{.items[0].spec.containers[0].image}'

```

- Examples

```bash
kubectl get nodes -o=jsonpath='{.items[*].metadata.name}'

```

```bash
kubectl get nodes -o=jsonpath='{.items[*].status.nodeInfo.architecture}'

```

```bash
kubectl get nodes -o=jsonpath='{.items[*].status.capatcity.cpu}'

```

- we can get two info with single command

```bash
kubectl get nodes -o=jsonpath='{.items[*].metadata.name}{.items[*].status.nodeInfo.architecture}'
```

- Adding a new line between infos

```bash
kubectl get nodes -o=jsonpath='{.items[*].metadata.name} {"\n"} {.items[*].status.nodeInfo.architecture}'

```

- Loops Range

```bash
kubectl get nodes -o=jsonpath='{range.items[*]} {.metadata.name} {"\t"} {.status.capacity.cpu} {"\n"} {end}'

```

- Custom Columns

```bash
kubectl get nodes -o=custom-columns=<COLUMN NAME>:<JSON PATH>

```

```bash
kubectl get nodes -o=custom-columns=<NODE>:.metadata.name

```

```bash
kubectl get nodes -o=custom-columns=NODE:.metadata.name, CPU:.status.capacity.cpu

```

- JSON Path for SORT

```bash
kubectl get nodes --sort-by=.metadata.name

kubectl get nodes --sort-by=.status.capacity.cpu

```

```bash 
kubectl get deploy -n admin2406 \ 
-o=custom-columns=DEPLOYMENT:.metadata.name,CONTAINER_IMAGE:.spec.template.spec.containers[0].image,READY_REPLICAS:.status.readyReplicas,NAMESPACE:.metadata.namespace \
--sort-by=.metadata.name
```
