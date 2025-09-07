# Containerd

https://github.com/containerd/containerd/blob/main/docs/getting-started.md

の option1 でインストール

バージョンの部分は確認して変更する

```bash
wget https://github.com/containerd/containerd/releases/download/v2.1.4/containerd-2.1.4-linux-amd64.tar.gz
sudo tar Cxzvf /usr/local containerd-2.1.4-linux-amd64.tar.gz
```$$

```bash
# systemdサービスファイルをダウンロード
sudo wget -O /etc/systemd/system/containerd.service https://raw.githubusercontent.com/containerd/containerd/main/containerd.service

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
