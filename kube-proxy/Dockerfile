FROM scratch
MAINTAINER Daniel Salinas <imsplitbit@gmail.com>
COPY kube-proxy /kube-proxy
VOLUME ["/etc/kubernetes", "/etc/ssl/certs", "/usr/sbin/iptables", "/lib64"]
ENTRYPOINT ["/kube-proxy"]
