## Install [docker-compose](https://docs.docker.com/compose/)
        sudo pip install docker-compose~=1.23.0
        docker run \
            -v /var/run/docker.sock:/var/run/docker.sock \
            -v "$PWD:/rootfs/$PWD" \
            -w="/rootfs/$PWD" \
            docker/compose:1.13.0 up
