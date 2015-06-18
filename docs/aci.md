# ACIs

The docker images produced by these docker files can be converted to ACIs.

## Convert Docker images to ACI using docker2aci

```
docker2aci docker://quay.io/kelseyhightower/kubelet:0.19.0
```

```
Downloading c6b09d8961e4: [====================================] 32 B/32 B
Downloading 57858edd3470: [====================================] 7.92 MB/7.92 MB
Downloading 1a4168fc39d8: [====================================] 32 B/32 B
Downloading 92c62d2e9e70: [====================================] 32 B/32 B

Converted volumes:
	name: "volume-nsenter", path: "/nsenter", readOnly: false
	name: "volume-rootfs", path: "/rootfs", readOnly: false
	name: "volume-usr", path: "/usr", readOnly: false
	name: "volume-var-lib-kubelet", path: "/var/lib/kubelet", readOnly: false
	name: "volume-var-run", path: "/var/run", readOnly: false
	name: "volume-etc-kubernetes", path: "/etc/kubernetes", readOnly: false
	name: "volume-etc-ssl-certs", path: "/etc/ssl/certs", readOnly: false
	name: "volume-lib64", path: "/lib64", readOnly: false
	name: "volume-sys", path: "/sys", readOnly: false
	name: "volume-var-lib-docker", path: "/var/lib/docker", readOnly: false

Generated ACI(s):
kelseyhightower-kubelet-0.19.0.aci
```

Repeat for the other images:

```
docker2aci docker://quay.io/kelseyhightower/kube-apiserver:0.19.0
```
```
docker2aci docker://quay.io/kelseyhightower/kube-controller-manager:0.19.0
```
```
docker2aci docker://quay.io/kelseyhightower/kube-proxy:0.19.0
```
```
docker2aci docker://quay.io/kelseyhightower/kube-scheduler:0.19.0
```

## Patch the ACI manifest using actool

TODO
