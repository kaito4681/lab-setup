# chico

# CNI プラグイン（Calico）のインストール

```bash
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.30.3/manifests/operator-crds.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.30.3/manifests/tigera-operator.yaml
```

```bash
curl https://raw.githubusercontent.com/projectcalico/calico/v3.30.3/manifests/custom-resources.yaml -O
```

spec: の中に以下の内容を追加

```yaml
proxy:
  httpProxy: http://ufproxy.b.cii.u-fukui.ac.jp:8080/
  httpsProxy: http://ufproxy.b.cii.u-fukui.ac.jp:8080/
  noProxy: .u-fukui.ac.jp,localhost,127.0.0.1,10.0.0.0/8,192.168.0.0/16,172.16.0.0/12,.local,.cluster.local
```

```bash
kubectl create -f custom-resources.yaml
```

```bash
watch kubectl get pods -n calico-system
```

```bash
NAMESPACE     NAME                READY   STATUS                  RESTARTS         AGE
kube-system   calico-node-txngh   1/1     Running                   0              54s
```

こうなれば OK

```bash
watch kubectl get tigerastatus
```

```bash
Every 2.0s: kubectl get tigerastatus     haselab-server-2080ti-2: Mon Sep  8 00:12:10 2025

NAME        AVAILABLE   PROGRESSING   DEGRADED   SINCE
apiserver   True        False         False      86s
calico      True        False         False      4m42s
goldmane    True        False         False      86s
ippools     True        False         False      65m
whisker     True        False         False      65m
```

こうなれば OK

# install cailcoctl

Calicoのポリシー管理や詳細な運用管理を行いたい場合はcalicoctlを入れる
管理用の端末それぞれに入れる


https://docs.tigera.io/calico/latest/operations/calicoctl/install
