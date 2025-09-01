# common setup

## 大学 proxy

```sh
echo 'export http_proxy="http://ufproxy.b.cii.u-fukui.ac.jp:8080"' >> ~/.bashrc
echo 'export no_proxy="localhost,127.0.0.1"' >> ~/.bashrc
source ~/.bashrc
echo 'Acquire::http::Proxy "http://ufproxy.b.cii.u-fukui.ac.jp:8080";' | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::https::Proxy "http://ufproxy.b.cii.u-fukui.ac.jp:8080";' | sudo tee -a /etc/apt/apt.conf
```

## apt

```sh
sudo apt install git curl vim
```

## ssh

```
sudo apt install openssh-server
```

<!-- ## remote desktop(optional)

設定アプリ > system > remote desktop > remote login をオンにする
繋いでみて，Error code 0x207 なら，export して rdp ファイルを以下のように修正

```diff
- use redirection server name:i:0
+ use redirection server name:i:1
``` -->



<!-- ## uv

[https://docs.astral.sh/uv/#highlights](https://docs.astral.sh/uv/#highlights)

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```sh
uv tool install ruff ty
``` -->

nvidia-driever

```bash
sudo ubuntu-drivers autoinstall
```


