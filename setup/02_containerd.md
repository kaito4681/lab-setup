# Containerd

https://github.com/containerd/containerd/blob/main/docs/getting-started.md

の option1 でインストール

バージョンの部分は確認して変更する

```bash
wget https://github.com/containerd/containerd/releases/download/v2.1.4/containerd-2.1.4-linux-amd64.tar.gz
sudo tar Cxzvf /usr/local containerd-2.1.4-linux-amd64.tar.gz
```

```bash
# systemdサービスファイルをダウンロード
sudo wget -O /etc/systemd/system/containerd.service https://raw.githubusercontent.com/containerd/containerd/main/containerd.service
```

```bash
# containerd用のプロキシ設定
sudo mkdir -p /etc/systemd/system/containerd.service.d
sudo tee /etc/systemd/system/containerd.service.d/http-proxy.conf <<EOF
[Service]
Environment="HTTP_PROXY=http://ufproxy.b.cii.u-fukui.ac.jp:8080/"
Environment="HTTPS_PROXY=http://ufproxy.b.cii.u-fukui.ac.jp:8080/"
Environment="NO_PROXY=.u-fukui.ac.jp,localhost,127.0.0.1,10.0.0.0/8,192.168.0.0/16,172.16.0.0/12,.local,.cluster.local"
EOF
```

# k8s 用の設定

https://kubernetes.io/ja/docs/setup/production-environment/container-runtimes/

```bash
containerd config default | sudo tee /etc/containerd/config.toml > /dev/null

# SystemdCgroupを有効化（Kubernetesで推奨）
# sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/g' /etc/containerd/config.toml
```

```yaml
[plugins.'io.containerd.cri.v1.runtime'.containerd.runtimes.runc.options]
```

に

```yaml
SystemdCgroup = true
```

を追加

```bash
# systemdを再読み込み
sudo systemctl daemon-reload

# containerdサービスを有効化
sudo systemctl enable --now containerd

# 確認
sudo systemctl status containerd
```

```bash
wget https://github.com/opencontainers/runc/releases/download/v1.3.0/runc.amd64
sudo install -m 755 runc.amd64 /usr/local/sbin/runc
```

```bash
wget https://github.com/containernetworking/plugins/releases/download/v1.8.0/cni-plugins-linux-amd64-v1.8.0.tgz
sudo mkdir -p /opt/cni/bin
sudo tar Cxzvf /opt/cni/bin cni-plugins-linux-amd64-v1.8.0.tgz
```
