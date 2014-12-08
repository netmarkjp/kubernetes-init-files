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

install
```
yum -y install docker git
git clone https://github.com/netmarkjp/kubernetes-init-files.git /opt/kubernetes-init-files
tar jxf /opt/kubernetes-init-files/usr/local/sbin.tar.bz2 -C /usr/local/.
cp -f /opt/kubernetes-init-files/usr/lib/systemd/system/* /usr/lib/systemd/system/.
cp -f /opt/kubernetes-init-files/etc/sysconfig/* /etc/sysconfig/.
systemctl daemon-reload
```

boot
```
systemctl start etcd.service
systemctl start flanneld.service
systemctl start kube-apiserver.service
systemctl start kube-controller-manager.service
systemctl start kube-proxy.service
systemctl start kube-scheduler.service
systemctl start kubelet.service
```

enable
```
systemctl enable etcd.service
systemctl enable flanneld.service
systemctl enable kube-apiserver.service
systemctl enable kube-controller-manager.service
systemctl enable kube-proxy.service
systemctl enable kube-scheduler.service
systemctl enable kubelet.service
```
