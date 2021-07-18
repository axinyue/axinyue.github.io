# Init检验镜像源配置

```
kubeadm init --config=config.conf 

输出： 
kubeadm config images list --config=config.conf 
registry.aliyuncs.com/google_containers/kube-apiserver:v1.21.0
registry.aliyuncs.com/google_containers/kube-controller-manager:v1.21.0
registry.aliyuncs.com/google_containers/kube-scheduler:v1.21.0
registry.aliyuncs.com/google_containers/kube-proxy:v1.21.0
registry.aliyuncs.com/google_containers/pause:3.4.1
registry.aliyuncs.com/google_containers/etcd:3.4.13-0
docker.io/coredns/coredns:1.8.4
```