# Kubernetes Docker Files

Build Docker images from upstream binaries

## etcd

```
mkdir -p /var/lib/etcd
```

### Run

```
sudo docker run --detach --net=host --privileged --name=etcd \
--restart=always \
--volume=/var/lib/etcd:/var/lib/etcd \
--volume=/usr/share/ca-certificates/:/etc/ssl/certs \
quay.io/coreos/etcd:v2.0.11 \
--advertise-client-urls http://127.0.0.1:2379 \
--data-dir /var/lib/etcd \
--listen-client-urls http://127.0.0.1:2379 \
--listen-peer-urls http://127.0.0.1:2380 \
--name etcd0
```

## kubelet

### Build

```
cp kubelet dockerfiles/kubelet/
```

```
cd dockerfiles/kubelet/
```

```
docker build -t quay.io/kelseyhightower/kubelet:0.19.0 .
```

### Run

```
sudo docker run --detach --net=host --name=kubelet \
--restart=always \
--volume=/:/rootfs:ro \
--volume=/etc/kubernetes/manifests:/etc/kubernetes/manifests \
--volume=/sys:/sys:ro \
--volume=/var/lib/docker/:/var/lib/docker:ro \
--volume=/var/lib/kubelet/:/var/lib/kubelet:rw \
--volume=/var/run:/var/run:rw \
quay.io/kelseyhightower/kubelet:0.19.0 \
--address=0.0.0.0 \
--api-servers=http://localhost:8080 \
--enable-server \
--hostname-override=127.0.0.1 \
--config=/etc/kubernetes/manifests \
--machine-id-file=/rootfs/etc/machine-id \
--v=2
```

## kube-apiserver

### Build

```
cp kube-apiserver dockerfiles/kube-apiserver/
```

```
cd dockerfiles/kube-apiserver/
```

```
docker build -t quay.io/kelseyhightower/kube-apiserver:0.19.0 .
```

### Run

```
sudo docker run --detach --net=host --name=kube-apiserver \
--restart=always \
quay.io/kelseyhightower/kube-apiserver:0.19.0 \
--etcd-servers=http://127.0.0.1:2379 \
--insecure-bind-address=0.0.0.0 \
--insecure-port=8080 \
--logtostderr=true \
--service-cluster-ip-range=10.200.20.0/24 \
--v=2
```

## kube-controller-manager

### Build

```
cp kube-controller-manager dockerfiles/kube-controller-manager/
```

```
cd dockerfiles/kube-controller-manager/
```

```
docker build -t quay.io/kelseyhightower/kube-controller-manager:0.19.0 .
```

### Run

```
sudo docker run --detach --net=host --name=kube-controller-manager \
--restart=always \
quay.io/kelseyhightower/kube-controller-manager:0.19.0 \
--logtostderr=true \
--master=http://127.0.0.1:8080 \
--v=2
```

## kube-proxy

### Build

```
cp kube-proxy dockerfiles/kube-proxy/
```

```
cd dockerfiles/kube-proxy/
```

```
docker build -t quay.io/kelseyhightower/kube-proxy:0.19.0 .
```

### Run

```
sudo docker run --detach --net=host --name=kube-proxy --privileged \
--restart=always \
--volume=/etc/kubernetes:/etc/kubernetes \
--volume=/usr/share/ca-certificates:/etc/ssl/certs \
--volume=/usr/sbin/iptables:/usr/sbin/iptables \
--volume=/lib64:/lib64 \
quay.io/kelseyhightower/kube-proxy:0.19.0 \
--logtostderr=true \
--master=http://127.0.0.1:8080 \
--v=2
```

## kube-scheduler

### Build

```
cp kube-scheduler dockerfiles/kube-scheduler/
```

```
cd dockerfiles/kube-scheduler/
```

```
docker build -t quay.io/kelseyhightower/kube-scheduler:0.19.0 .
```

### Run

```
sudo docker run --detach --net=host --name=kube-scheduler \
--restart=always \
--volume /etc/kubernetes:/etc/kubernetes \
--volume /usr/share/ca-certificates/:/etc/ssl/certs \
quay.io/kelseyhightower/kube-scheduler:0.19.0 \
--logtostderr=true \
--master=http://127.0.0.1:8080 \
--v=2
```

## kubectl

### Build

```
docker build -t quay.io/kelseyhightower/kubectl:0.19.0 -f kubectl/Dockerfile
```

### Run

```
sudo docker run -t -i --net=host quay.io/kelseyhightower/kubectl:0.19.0 kubectl
```
