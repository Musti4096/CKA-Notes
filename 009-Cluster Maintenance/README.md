# Cluster Maintenance

## Operating System Uprgrade

- Pod Eviction Timeout

```bash
kube-controller-manager --pod-eviction-timeout=5m0s #that is default timeout value
```

- Drain the node ( if node will be out of service soon )

```bash
kubectl drain node-1
```

- Cordon and uncordon Nodes (if node will be out of service soon )

```bash
kubectl cordon node-2
kubectl uncordon node-1
```

## Cluster upgrade

- kubeadm upgrade

```bash
apt-get upgrade -y kubeadm=1.12.0-00 # we should upgrade one by one (minor updates)

kubeadm upgrade apply v1.12.0
```

- after kubeadm upgrade opr. we should updgrade kubelet

```bash
apt-get upgrade -y kubelet=1.12.0-00 # we should upgrade one by one (minor updates)

systemctl restart kubelet
```

- for nodes

```bash
kubectl drain node1

apt-get upgrade -y kubeadm=1.12.0-00

apt-get upgrade -y kubelet=1.12.0-00

kubeadm upgrade node1 config --kubelet-version v1.12.0

systemctl restart kubelet

kubectl uncordon node1
```

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.20.0-00 && \
apt-mark hold kubeadm

sudo kubeadm upgrade apply v1.20.07

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.20.0-00 kubectl=1.20.0-00 && \
apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.20.0-00 && \
apt-mark hold kubeadm

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.20.0-00 kubectl=1.20.0-00 && \
apt-mark hold kubelet kubectl

## BackUp

```shell
kubectl get all --all-namespaces -o yaml >all-deploy-services.yaml
```

- etcd backup

```shell
etcdctl snapshot save snapshot.db  #get snapshot from etcd

service kube-apiserverstop #stop api server

etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd-from-backup #restore etcd from backup

systemctl deamon-reload

service etcd restart

service kube-apiserver start
```

Working with ETCDCTL

etcdctl is a command line client for etcd.

In all our Kubernetes Hands-on labs, the ETCD key-value database is deployed as a static pod on the master. The version used is v3.

To make use of etcdctl for tasks such as back up and restore, make sure that you set the ETCDCTL_API to 3.

You can do this by exporting the variable ETCDCTL_API prior to using the etcdctl client. This can be done as follows:

`export ETCDCTL_API=3`

For example, if you want to take a snapshot of etcd, use:

`etcdctl snapshot save -h` and keep a note of the mandatory global options.

Since our ETCD database is TLS-Enabled, the following options are mandatory:

--cacert verify certificates of TLS-enabled secure servers using this CA bundle

--cert identify secure client using this TLS certificate file

--endpoints=[127.0.0.1:2379] This is the default as ETCD is running on master node and exposed on localhost 2379.

--key identify secure client using this TLS key file

Similarly use the help option for snapshot restore to see all available options for restoring the backup.

`etcdctl snapshot restore -h`

For a detailed explanation on how to make use of the etcdctl command line tool and work with the -h flags, check out the solution video for the Backup and Restore Lab.

```bash
kubectl describe po etcd-controlplane -n kubesystem #etcd descriptions
```

- export etcdctl version

```bash
export ETCDCTL_API=3
```

- backup etcd

```bash
etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db
```

- restore from backup

```bash
etcdctl --data-dir /var/lib/etcd-from-backup \
snapshot restore /opt/snapshot-pre-boot.db
```

- after restoring we should update etcd.yaml file under /etc/kubernetes/manifest
  Because we use now etcd backup from /var/lib/etcd-from-backup
  we should update this directory
