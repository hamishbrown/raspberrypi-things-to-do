## Install your own [Git server](https://gogs.io/)
        docker run -d --name gogs-git-server \
            --publish 8022:22 \
            --publish 3000:3000 \
            --volume `pwd`/gogs-data/:/data \
            hypriot/rpi-gogs-raspbian
