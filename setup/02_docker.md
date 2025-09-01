# docker

## install

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Rootless 化

https://docs.docker.com/engine/security/rootless/

```bash
sudo apt-get install -y dbus-user-session
sudo apt-get install -y uidmap
sudo apt-get install -y systemd-container
```

```bash
sudo systemctl disable --now docker.service docker.socket
sudo rm /var/run/docker.sock
sudo reboot
```

```bash
dockerd-rootless-setuptool.sh install
```

(dockerd-rootless-setuptool.sh は /usr/bin/にあり，PATH はすでに通っている)

## test

```bash
docker run hello-world
```
