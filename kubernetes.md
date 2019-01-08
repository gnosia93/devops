https://hiseon.me/2018/08/23/ubuntu-kubernetes-install/

```
Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 192.168.29.122:6443 --token tqwyhc.39tgs5rkl2vunf6t --discovery-token-ca-cert-hash sha256:65c575a62bc097fbd67435e45515bcb1a4884c9fa6bfdf8c3dcd4187ea560519
```


# MicroK8s #

### 설치 ###

https://microk8s.io/#quick-start

### 대시보드 ###

https://github.com/kubernetes/dashboard

```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yam

```
