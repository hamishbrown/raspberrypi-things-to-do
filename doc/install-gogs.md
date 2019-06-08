## Host your own Git server*
* https://gogs.io/
* https://hub.docker.com/r/hypriot/rpi-gogs-raspbian/
```
        docker run -d --name gogs-git-server \
            --publish 8022:22 \
            --publish 3000:3000 \
            --volume `pwd`/gogs-data/:/data \
            hypriot/rpi-gogs-raspbian
```
*Requires [Docker](./doc/install-docker.md)
