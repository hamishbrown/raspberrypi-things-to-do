## Install [DuckDNS](https://www.duckdns.org/)
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
