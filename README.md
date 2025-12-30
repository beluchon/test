
```
sudo apt-get update
sudo apt-get upgrade -y
```

docker et docker compose

```# Add Docker's official GPG key:
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

lancer aux démarrage docker

```# Add Docker's official GPG key:
sudo systemctl start docker
```

puis dockge

```
sudo mkdir -p /opt/stacks /opt/dockge
cd /opt/dockge

sudo curl https://raw.githubusercontent.com/louislam/dockge/master/compose.yaml --output compose.yaml

sudo docker compose up -d
```
faite 

```
hostname -I
```

et copier la première ip

puis aller sur https://votre-ip:5001

une fois l'interface de dockge ouvert regarder https://github.com/beluchon/self_host_fr/blob/main/2%20nginx%20et%20cloudflare.md
