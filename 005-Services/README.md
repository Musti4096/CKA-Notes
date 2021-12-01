# Kubernetes CLI commands

## Services

### Service Types

- NodePort > Serves from node ports

  - NodePort
  - Port
  - TargetPort

- ClusterIP > Serves inside of Cluster

  - We can use ClusterIP to let the microservices communicate each other

- LoadBalancer > serves on cloud based Loadbalancer

- Create a configuration yml file with cli command

```bash
kubectl expose pod nginx --port=80 nginx-service --type=NodePort --dry-run=client -o yaml

kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
```
