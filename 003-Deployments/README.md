# Kubernetes CLI commands

## Deployments

- Create an NGINX Pod

```bash
kubectl run nginx --image=nginx
```

- Generate POD manifest YAML file (-o yaml) with dry run

```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

- Create a deployment

```bash
kubectl create deployment --image=nginx nginx
```

- Generate Deployment YAML file (-o yaml) with dry-run

```bash
kubectl create deployment --image=nginx nginx
--dry-run=client -o yaml
```

- Generate Deployment YAML file (-o yaml) with dry-run with 4 replicas

```bash
kubectl create deployment --replicas=4 --image=nginx nginx
--dry-run=client -o yaml > nginx-deployment.yaml
```

## Edit Deployments

With Deployments you can easily edit any field/property of the POD template. Since the pod template is a child of the deployment specification, with every change the deployment will automatically delete and create a new pod with the new changes. So if you are asked to edit a property of a POD part of a deployment you may do that simply by running the command

```bash
kubectl edit deployment my-deployment
```
