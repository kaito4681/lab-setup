# cluster 作成

<!-- ## kubeadm init 設定ファイル作成

```bash
cat <<EOF > kubeadm-config.yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
kubernetesVersion: v1.33.4
controlPlaneEndpoint: "10.0.87.36:6443"
networking:
  podSubnet: 192.168.0.0/16
  serviceSubnet: 10.96.0.0/12
---
apiVersion: kubeadm.k8s.io/v1beta3
kind: InitConfiguration
nodeRegistration:
  kubeletExtraArgs:
    cluster-dns: "10.96.0.10"
    cluster-domain: "cluster.local"
---
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
serverTLSBootstrap: true
EOF
``` -->

<!-- ```bash
sudo kubeadm init --config=kubeadm-config.yaml　--pod-network-cidr=192.168.0.0/16
``` -->

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

出力されたコマンド

```bash
# kubeadm join 10.0.87.36:6443 --token y3wpq1.ntctevpzoelgffal \
#  --discovery-token-ca-cert-hash sha256:eebd042bd1016f01b0de04902a52612072b71df4219e01b62e4d1831fe315597
kubeadm join 10.0.87.36:6443 --token g6kzys.smiub8heizjqwd5e \
        --discovery-token-ca-cert-hash sha256:85ac860ae826f318bd0b6e0ea8c33f7556f026451b6135f64d00e610b3c6f22f
```

master のみで実行

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

token 再発行と command 表示

```bash
sudo kubeadm token create --print-join-command
```
