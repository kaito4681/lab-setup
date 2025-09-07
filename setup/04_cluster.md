# cluster 作成

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

出力されたコマンド

```bash
# kubeadm join 10.0.87.36:6443 --token y3wpq1.ntctevpzoelgffal \
#  --discovery-token-ca-cert-hash sha256:eebd042bd1016f01b0de04902a52612072b71df4219e01b62e4d1831fe315597
kubeadm join 10.0.87.36:6443 --token u5envm.xcxpf5g6fwdvid6r \
        --discovery-token-ca-cert-hash sha256:715c59757639d09653bed4e31bb83b3a88a5612020ba826ee6030b2bf02faf91
```

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

$HOME/.kube/config を他の worker に送る

# CNI プラグイン（Calico）のインストール

```bash
kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
```
