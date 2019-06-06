## Install DuckDNS*
* https://www.duckdns.org/
* https://hub.docker.com/r/linuxserver/duckdns/
---
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
---
*Requires [Docker](./install-docker.md)
