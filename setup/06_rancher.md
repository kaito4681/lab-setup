# Rancher

https://ranchermanager.docs.rancher.com/getting-started/installation-and-upgrade/install-upgrade-on-a-kubernetes-cluster

## 1. Helm リポジトリ追加

```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
helm repo update
```

## 2. cattle-system 名前空間作成

```bash
kubectl create namespace cattle-system
```

## 3. cert-manager 導入（SSL 証明書管理）

```bash
# If you have installed the CRDs manually, instead of setting `installCRDs` or `crds.enabled` to `true` in your Helm install command, you should upgrade your CRD resources before upgrading the Helm chart:

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.18.2/cert-manager.crds.yaml

# Add the Jetstack Helm repository

helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache

helm repo update

# Install the cert-manager Helm chart

helm install cert-manager jetstack/cert-manager \
 --namespace cert-manager \
 --create-namespace \
 --set crds.enabled=true
```

error になるがインストールできているっぽい

```bash
helm install cert-manager jetstack/cert-manager   --namespace cert-manager   --create-namespace   --set crds.enabled=true
Error: INSTALLATION FAILED: failed post-install: 1 error occurred:
        * timed out waiting for the condition
```

<!-- https://cert-manager.io/docs/installation/helm/

```bash
helm install \
  cert-manager oci://quay.io/jetstack/charts/cert-manager \
  --version v1.18.2 \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true
``` -->

## 4. cert-manager 起動確認

```bash
kubectl get pods --namespace cert-manager
```

## 5. Rancher インストール

↓ 競合直すためにポート変更したら動いた．詳しく調べた方が良さそう

```bash
helm upgrade --install cert-manager jetstack/cert-manager \
--namespace cert-manager --create-namespace \
--set webhook.hostNetwork=true \
--set webhook.securePort=10260
```

### オプション A: 自己署名証明書（開発環境向け）

一旦こっち

helm upgrade rancher rancher-stable/rancher \
 --namespace cattle-system \
 --set hostname=rancher.my.org \
 --set bootstrapPassword=admin
 --set proxy=${http_proxy}

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.local \
  --set ingress.tls.source=rancher \
  --set bootstrapPassword=admin
```

実行結果

``
haselab@haselab-server-2080ti-2:~$ helm install rancher rancher-stable/rancher \
 --namespace cattle-system \
 --set hostname=rancher.local \
 --set ingress.tls.source=rancher \
 --set bootstrapPassword=admin
NAME: rancher
LAST DEPLOYED: Sun Sep 7 18:19:48 2025
NAMESPACE: cattle-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Rancher Server has been installed.

NOTE: Rancher may take several minutes to fully initialize. Please standby while Certificates are being issued, Containers are started and the Ingress rule comes up.

Check out our docs at https://rancher.com/docs/

## First Time Login

If you provided your own bootstrap password during installation, browse to https://rancher.local to get started.
If this is the first time you installed Rancher, get started by running this command and clicking the URL it generates:

```

echo https://rancher.local/dashboard/?setup=$(kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{.data.bootstrapPassword|base64decode}}')

```

To get just the bootstrap password on its own, run:

```

kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{.data.bootstrapPassword|base64decode}}{{ "\n" }}'

```

Happy Containering!

```

```

### オプション B: Let's Encrypt（本番環境向け）

メアドもらえたら，これにしたい
有効期限切れたら自動更新なのかも調べる

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.local \
  --set ingress.tls.source=letsEncrypt \
  --set letsEncrypt.email=your-email@example.com \
  --set letsEncrypt.environment=prod \
  --set replicas=1
```

## 6. Rancher 起動確認

```bash
kubectl -n cattle-system get pods
kubectl -n cattle-system get svc
```

## 7. 初期パスワード取得

```bash
kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{.data.bootstrapPassword|base64decode}}{{"\n"}}'
```

## 8. アクセス方法

### ローカルアクセス（kubectl port-forward）

```bash
kubectl port-forward -n cattle-system svc/rancher 8443:443
```

ブラウザで `https://localhost:8443` にアクセス

### 外部アクセス（NodePort）

```bash
kubectl patch svc rancher -n cattle-system -p '{"spec":{"type":"NodePort"}}'
kubectl get svc rancher -n cattle-system
```

表示された NodePort でアクセス（例：`https://ノードIP:30443`）
