## Keep all your containers updated with Watchtower*
* https://containrrr.github.io/watchtower/
* https://hub.docker.com/r/containrrr/watchtower
```
        docker run -d \
            --name watchtower \
            -e WATCHTOWER_CLEANUP=true \
            -v /var/run/docker.sock:/var/run/docker.sock \
            containrrr/watchtower:armhf-latest
```
*Requires [Docker](./doc/install-docker.md)
