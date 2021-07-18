## Install Kubeadm

1. 创建repo文件并写入url,快速命令如下
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```
2. yum update更新

3. install 管理工具
```
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
```
4. 容器环境配置
这里使用Docker，需要先安装Docker
```
sudo mkdir /etc/docker
cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

* 注意如果通过systemctl重启失败，你可能需要修改/usr/lib/systemd/system/docker.service的ExecStart并指定为/usr/bin/dockerd。 或者你可以尝试直接输入dockerd 尝试启动


5. kubeadm 初始化(自定义repo绕过代理)

config.conf, 通过：kubeadm config print init-defaults 输出并添加镜像库
```
apiVersion: kubeadm.k8s.io/v1beta2
bootstrapTokens:
- groups:
  - system:bootstrappers:kubeadm:default-node-token
  token: abcdef.0123456789abcdef
  ttl: 24h0m0s
  usages:
  - signing
  - authentication
kind: InitConfiguration
localAPIEndpoint:
  advertiseAddress: 1.2.3.4
  bindPort: 6443
nodeRegistration:
  criSocket: /var/run/dockershim.sock
  name: node
  taints: null
---
apiServer:
  timeoutForControlPlane: 4m0s
apiVersion: kubeadm.k8s.io/v1beta2
certificatesDir: /etc/kubernetes/pki
clusterName: kubernetes
controllerManager: {}
dns:
  type: CoreDNS
  imageRepository: "docker.io/coredns"
  imageTag: "1.8.4"

etcd:
  local:
    dataDir: /var/lib/etcd
imageRepository: registry.aliyuncs.com/google_containers
kind: ClusterConfiguration
kubernetesVersion: 1.21.0
networking:
  dnsDomain: cluster.local
  serviceSubnet: 10.96.0.0/12
scheduler: {}

```

通过kubeadm init --config=config.yml 执行初始化，请先确保kubectl正在运行中. 
```
  # 注意 registry.aliyuncs.com/google_containers未包含coredns这里修改repo为
  imageRepository: "docker.io/coredns"
  imageTag: "1.8.4"
```
* [coredns参考](https://kubernetes.io/zh/docs/reference/setup-tools/kubeadm/kubeadm-init-phase/)

* [kubadmin install参考](https://kubernetes.io/zh/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

* [kubeadmin init 默认配置](https://kubernetes.io/zh/docs/reference/setup-tools/kubeadm/kubeadm-config/#cmd-config-print-init-defaults)
* [kubeadmin init 初始化配置](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/#config-file)

* [kubeadmin 分阶段初始化](https://kubernetes.io/zh/docs/reference/setup-tools/kubeadm/kubeadm-init-phase/)


* [删除集群](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#tear-down)