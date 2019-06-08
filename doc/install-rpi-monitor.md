## Install RpiMonitor*
* https://xavierberger.github.io/RPi-Monitor-docs/01_features.html)
```
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
*Requires [Docker](./install-docker.md)
