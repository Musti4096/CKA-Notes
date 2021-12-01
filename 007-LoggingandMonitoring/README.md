# Logging & Monitoring

## Metrics Server

- Setting up MetricsServer

```bash
minicube addons enable metrics-server
```

- other clusters

```bash
git clone https://github.com/kubernetes-incubator/metrics-server

kubectl create -f deploy/1.8+/
```

- monitor with MetricsServer

```bash
kubectl top node
kubectl top pod
```

## Logs Kubernetes (Application Logs)

- Event Simulator

```bash
docker logs -f ecf   #shows us docker container logs

kubectl create -f  event-simulator.yaml

kubectl logs -f event-simulator-pod
```

```bash
kubectl logs webapp-1  #show logs for pods
kubectl logs webapp-2 -c simple-webapp  #show logs for one of the container inside of pod
```
