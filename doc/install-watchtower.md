## Keep everything updated with [Watchtower](https://containrrr.github.io/watchtower/)
        docker run -d \
            --name watchtower \
            -e WATCHTOWER_CLEANUP=true \
            -v /var/run/docker.sock:/var/run/docker.sock \
            containrrr/watchtower:armhf-latest
