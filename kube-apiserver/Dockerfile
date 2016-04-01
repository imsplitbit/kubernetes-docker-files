FROM scratch
MAINTAINER Daniel Salinas <imsplitbit@gmail.com>
COPY kube-apiserver /kube-apiserver
VOLUME ["/etc/kubernetes", "/etc/ssl/certs", "/var/run/kubernetes"]
ENTRYPOINT ["/kube-apiserver"]
