# Networking

## Switching Routing

- show ethernet card info

```bash
ip link
```

- add ip address to interface card

```bash
ip addr add 192.168.1.10/24 dev eth0
```

- show route table

```bash
ip route
```

- add a route to route table

```bash
ip route add 192.168.1.0/24 via 192.168.2.1
```

- ip_forward

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward

etc/sysctl.conf file > nt.ipv4.ip_forward=1
```

## DNS

describe one ip address as a db_server

```bash
cat >> /etc/hosts # go this file

192.168.1.11      db   #enter this record as a db server address
```

- describe DNS server on linux machine

```bash
cat /etc/resolv.conf
nameservr 192.168.1.100
```

- query dns name

```bash
nslookup www.google.com

dig google.com
```

## FAQ Command

```bash
pfconfig #shows interfacess

ip link # show interfaces details

ip route | ip r  #shows defautl gateway

netstat -natulp | grep kube-scheduler #shows which port kubescheduler listens.
```

## CNI Weave

```bash
ps -aux | grep kubelet # shows that which network plugin kubelet uses

cd /opt/cni/bin # in this directory we can find all binaries related network plugins

cd /etc/cni/net.d  # under this directory we can find related network plugin configuration (10-weace.conf)

cat /etc(cni/net.d/10-weave.conf # we could describe all details about network plugin)
```

## Deploying Network Solution

```bash
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

```

https://www.weave.works/docs/net/latest/kubernetes/kube-addon/

## Ip Adress Management

```bash

ssh node03 ip r # check the default gateway on worker node with weave network

```

## Service Networking

```bash
kubectl get nodes -o wide

```

## DNS and CoreDNS in K8s

- coreDNS conf file /etc/coreDns

```bash

kubectl exec -it hr -- nslookup mysql.payroll > /root/CKA/nslookup.out

```

cluster.local > domain_name
webapp
webapp.default
webapp.default.svc
webapp.default.svc.cluster.local

## Ingress
