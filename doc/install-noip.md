## Install NoIP daemon*
* https://www.noip.com/
* https://hub.docker.com/r/hypriot/rpi-noip
```
        docker run -ti -v "noip:/usr/local/etc/" hypriot/rpi-noip noip2 -C
        docker run --name noip -v "noip:/usr/local/etc/" --restart=always hypriot/rpi-noip
```
*Requires [Docker](./install-docker.md)
