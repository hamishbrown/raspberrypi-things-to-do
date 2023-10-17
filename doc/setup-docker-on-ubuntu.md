## Install useful tools
```
sudo apt install wget mc ncdu htop avahi-daemon
```

## Install docker
```
sudo apt install docker.io
```
Start docker as a service
```
sudo systemctl enable --now docker
```
Add ubuntu user to docker group
```
sudo usermod -aG docker ubuntu
```

## Install docker-compose
```
sudo apt install build-essential libssl-dev libffi-dev python3-pip

sudo pip3 install docker-compose
```

## Setup Portainer and Netdata
#### https://www.portainer.io/
#### https://www.netdata.cloud/open-source/

Create ```docker-compose.yml```

```
nano docker-compose.yml
```
Copy and paste the following:
```
version: '2'

volumes:
  portainer-data:

services:

  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    ports:
      - 9000:9000
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer-data:/data
    restart: always

  netdata:
    image: netdata/netdata:latest
    container_name: netdata
    ports:
      - 19999:19999
    restart: always
```
