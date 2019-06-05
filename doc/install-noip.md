## Install [NoIP](https://www.noip.com/) daemon
        docker run -ti -v "noip:/usr/local/etc/" hypriot/rpi-noip noip2 -C
        docker run --name noip -v "noip:/usr/local/etc/" --restart=always hypriot/rpi-noip
