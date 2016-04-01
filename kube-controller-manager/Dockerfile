FROM scratch
MAINTAINER Daniel Salinas <imsplitbit@gmail.com>
COPY kube-controller-manager /kube-controller-manager
VOLUME ["/etc/kubernetes", "/etc/ssl/certs"]
ENTRYPOINT ["/kube-controller-manager"]
