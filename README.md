Kubernetes init files
=============================

# Includes

- binaries for linux(x86_64)
    - Kubernetes v0.5.3
    - etcd 0.4.6
    - etcdctl 0.4.5
    - flannel 0.1.0
- systemd setting file
    - /usr/lib/systemd/system/*.service
    - /etc/sysconfig/*

# Usage

## Install

```
yum -y install docker git bzip2
git clone https://github.com/netmarkjp/kubernetes-init-files.git /opt/kubernetes-init-files
tar jxf /opt/kubernetes-init-files/usr/local/sbin.tar.bz2 -C /usr/local/.
yes | cp /opt/kubernetes-init-files/usr/lib/systemd/system/* /usr/lib/systemd/system/.
yes | cp /opt/kubernetes-init-files/etc/sysconfig/* /etc/sysconfig/.
systemctl daemon-reload
```

init for flannel
```
systemctl start etcd.service
etcdctl mk /coreos.com/network/config '{"Network":"172.17.0.0/16"}'
```

boot
```
systemctl start etcd.service
systemctl start flanneld.service
systemctl start docker.service
systemctl start kube-apiserver.service
systemctl start kube-controller-manager.service
systemctl start kube-proxy.service
systemctl start kube-scheduler.service
systemctl start kubelet.service
```

## Enable daemons

enable for Kubernetes Master + Minion
```
systemctl enable etcd.service
systemctl enable flanneld.service
systemctl enable docker.service
systemctl enable kube-apiserver.service
systemctl enable kube-controller-manager.service
systemctl enable kube-proxy.service
systemctl enable kube-scheduler.service
systemctl enable kubelet.service
```

enable for Kubernetes Master only
```
systemctl enable etcd.service
systemctl enable flanneld.service
systemctl enable docker.service
systemctl enable kube-apiserver.service
systemctl enable kube-controller-manager.service
systemctl enable kube-scheduler.service
systemctl enable kubelet.service
```

enable for Kubernetes Minion only
```
systemctl enable etcd.service
systemctl enable flanneld.service
systemctl enable docker.service
systemctl enable kube-proxy.service
systemctl enable kubelet.service
```
