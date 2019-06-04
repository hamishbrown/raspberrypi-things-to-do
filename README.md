raspberrypi-things-to-do
========================

A collection of usefully random things to do with a Raspberry Pi.

* Install [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)
* Install [Docker](https://www.docker.com/)
  ```
  curl -sSL https://get.docker.com | sh
  sudo usermod -aG docker pi
  ```
* Install [Python](https://www.python.org/) and [Pip](https://www.pypa.io)
  `sudo apt-get install -y python python-pip`
* Install [docker-compose](https://docs.docker.com/compose/)
  `sudo pip install docker-compose~=1.23.0`
* Install [Portainer] (https://www.portainer.io/)
  `docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer`
* Install your own [Git server](https://gogs.io/)
  ``docker run -d --name gogs-git-server --publish 8022:22 --publish 3000:3000 --volume `pwd`/gogs-data/:/data hypriot/rpi-gogs-raspbian``
* Keep everything updated with [Watchtower](https://containrrr.github.io/watchtower/)
   ```
   docker run -d \
     --name watchtower \
     -e WATCHTOWER_CLEANUP=true \
     -v /var/run/docker.sock:/var/run/docker.sock \
     containrrr/watchtower:armhf-latest
   ```

* Reboot
