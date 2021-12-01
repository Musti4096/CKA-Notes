# Kubernetes CLI POD commands

## Pods

- Create pods without yml file

```bash
kubectl run nginx --image=nginx
```

- Create pods

```bash
kubectl create -f pod-deployment.yml
```

- Inspect the pods

```bash
kubectl describe pod webapp

kubectl get pod webapp -o wide
```

- Delete pods

```bash
kubectl delete pod webapp
```

- Edit pods yml file and get it

```bash
kubectl edit pod webapp
```

## Editing Pods

For example you cannot edit the environment variables, service accounts, resource limits (all of which we will discuss later) of a running pod. But if you really want to, you have 2 options:

1. Run the kubectl edit pod <pod name> command. This will open the pod specification in an editor (vi editor). Then edit the required properties. When you try to save it, you will be denied. This is because you are attempting to edit a field on the pod that is not editable. A copy of the file with your changes is saved in a temporary location as shown above.

You can then delete the existing pod by running the command:

```bash
kubectl delete pod webapp
```

Then create a new pod with your changes using the temporary file

```bash
kubectl create -f /tmp/kubectl-edit-ccvrq.yaml
```

2. The second option is to extract the pod definition in YAML format to a file using the command

```bash
kubectl get pod webapp -o yaml > my-new-pod.yaml
```

Then make the changes to the exported file using an editor (vi editor). Save the changes

```bash
vi my-new-pod.yaml
```

Then delete the existing pod

```bash
kubectl delete pod webapp
```

Then create a new pod with the edited file

````bash
kubectl create -f my-new-pod.yaml```
````
