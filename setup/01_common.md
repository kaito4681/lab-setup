# common setup

## 大学 proxy

```sh
echo 'export HTTPS_PROXY="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export HTTP_PROXY="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export FTP_proxy="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export https_proxy="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export http_proxy="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export ftp_proxy="http://ufproxy.b.cii.u-fukui.ac.jp:8080/"' >> ~/.bashrc
echo 'export no_proxy=".u-fukui.ac.jp,localhost,127.0.0.1,10.0.0.0/8,192.168.0.0/16,172.16.0.0/12,.local,.cluster.local"' >> ~/.bashrc
source ~/.bashrc
echo 'Acquire::http::Proxy "http://ufproxy.b.cii.u-fukui.ac.jp:8080/";' | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::https::Proxy "http://ufproxy.b.cii.u-fukui.ac.jp:8080/";' | sudo tee -a /etc/apt/apt.conf
```

## apt

```sh
sudo apt install git curl vim
```

## ssh

```
sudo apt install openssh-server
```

nvidia-driever

```bash
sudo ubuntu-drivers autoinstall
```
