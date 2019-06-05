# raspberrypi-things-to-do

A collection of usefully random things to do with a Raspberry Pi.

#### Install [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)

#### Install [Docker](https://www.docker.com/)
        curl -sSL https://get.docker.com | sh
        sudo usermod -aG docker pi

#### Install [Python](https://www.python.org/) and [Pip](https://www.pypa.io)
        sudo apt-get install -y python python-pip

#### Install [docker-compose](https://docs.docker.com/compose/)
        sudo pip install docker-compose~=1.23.0
        docker run \
            -v /var/run/docker.sock:/var/run/docker.sock \
            -v "$PWD:/rootfs/$PWD" \
            -w="/rootfs/$PWD" \
            docker/compose:1.13.0 up

#### Install [Portainer](https://www.portainer.io/)
        docker run -d -p 9000:9000 \
            -v /var/run/docker.sock:/var/run/docker.sock \
            -v portainer_data:/data \
            portainer/portainer

#### Install your own [Git server](https://gogs.io/)
        docker run -d --name gogs-git-server \
            --publish 8022:22 \
            --publish 3000:3000 \
            --volume `pwd`/gogs-data/:/data \
            hypriot/rpi-gogs-raspbian

#### Keep everything updated with [Watchtower](https://containrrr.github.io/watchtower/)
        docker run -d \
            --name watchtower \
            -e WATCHTOWER_CLEANUP=true \
            -v /var/run/docker.sock:/var/run/docker.sock \
            containrrr/watchtower:armhf-latest

#### Install [NoIP](https://www.noip.com/) daemon
        docker run -ti -v "noip:/usr/local/etc/" hypriot/rpi-noip noip2 -C
        docker run --name noip -v "noip:/usr/local/etc/" --restart=always hypriot/rpi-noip

#### Install [DuckDNS](https://www.duckdns.org/)
        docker create \
            --name=duckdns \
            -e PUID=1000 \
            -e PGID=1000 \
            -e TZ=UTC \
            -e SUBDOMAINS=<SUB_DOMAIN>.duckdns.org \
            -e TOKEN=<DUCK_DNS_TOKEN> \
            -e LOG_FILE=false \
            -v /home/pi/docker/volumes/duckdns/config:/config \
            --restart unless-stopped \
            linuxserver/duckdns

#### Host your own [Tomcat](https://hub.docker.com/_/tomcat) webapp

In the directory containing your WAR file

        nano Dockerfile

Copy and Paste the following code

        FROM tomcat:8.0
        COPY ./<YOUR_WEB_APP_NAME>.war /usr/local/tomcat/webapps/

Save and Exit the file

        <Ctrl-x>y<Enter>

Build `<YOUR_IMAGE_NAME>`

        docker build -t <YOUR_IMAGE_NAME> .

Run `<YOUR_CONTAINER_NAME>`

        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>

Access at

        http://<PI_IP_ADDR>:8080/<YOUR_WEB_APP_NAME>

#### Host your own [Apache](https://hub.docker.com/_/httpd) simple HTML website

Create a directory for your website files called `public-html`

        mkdir public-html

Copy your website files (.html, .js, .css) into `public-html`

Create `Dockerfile`

        nano Dockerfile

Copy and Paste the following code

        FROM httpd:2.4
        COPY ./public-html/ /usr/local/apache2/htdocs/

Save and Exit the file

        <Ctrl-x>y<Enter>

Build `<YOUR_IMAGE_NAME>`

        docker build -t <YOUR_IMAGE_NAME> .

Run `<YOUR_CONTAINER_NAME>`

        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>

Access at

        <http://<PI_IP_ADDR>/<YOUR_WEB_SITE_PAGE>

#### Install [Pi-Hole](https://pi-hole.net/)
Create `docker-compose.yml`

```yaml
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "80:80/tcp"
      - "443:443/tcp"
    environment:
      TZ: 'Europe/Dublin'
      # WEBPASSWORD: 'set a secure password here or it will be random'
    # Volumes store your data between container upgrades
    volumes:
       - './etc-pihole/:/etc/pihole/'
       - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    dns:
      - 127.0.0.1
      - 1.1.1.1
    # Recommended but not required (DHCP needs NET_ADMIN)
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```
Start with `docker-compose up`

#### Install [RpiMonitor](https://xavierberger.github.io/RPi-Monitor-docs/01_features.html)

```Docker
docker run --device=/dev/vchiq \
    --volume=/opt/vc:/opt/vc \
    --volume=/boot:/boot \
    --volume=/sys:/dockerhost/sys:ro \
    --volume=/etc:/dockerhost/etc:ro \
    --volume=/proc:/dockerhost/proc:ro \
    --volume=/usr/lib:/dockerhost/usr/lib:ro \
    -p=8888:8888 \
    --name="rpi-monitor" \
    -d  michaelmiklis/rpi-monitor:latest
```

#### Reboot your Pi

        sudo reboot
