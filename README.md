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

1. In the directory containing your WAR file
        nano Dockerfile
2. Copy and Paste the following code
        FROM tomcat:8.0
        COPY ./<YOUR_WEB_APP_NAME>.war /usr/local/tomcat/webapps/
3. Save and Exit the file
        <Ctrl-x>y<Enter>
4. Build `<YOUR_IMAGE_NAME>`
        docker build -t <YOUR_IMAGE_NAME> .
5. Run `<YOUR_CONTAINER_NAME>`
        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>
6. Access at
        http://<PI_IP_ADDR>:8080/<YOUR_WEB_APP_NAME>

#### Host your own [Apache](https://hub.docker.com/_/httpd) simple HTML website

1. Create a directory for your website files called `'public-html'`
        mkdir public-html
2. Copy your website files (.html, .js, .css) into `'public-html'`

3. Create `Dockerfile`
        nano Dockerfile
4. Copy and Paste the following code
        FROM httpd:2.4
        COPY ./public-html/ /usr/local/apache2/htdocs/
5. Save and Exit the file
        <Ctrl-x>y<Enter>
6. Build `<YOUR_IMAGE_NAME>`
        docker build -t <YOUR_IMAGE_NAME> .
7. Run `<YOUR_CONTAINER_NAME>`
        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>
8. Access at
        <http://<PI_IP_ADDR>/<YOUR_WEB_SITE_PAGE>

#### Reboot
    sudo reboot
