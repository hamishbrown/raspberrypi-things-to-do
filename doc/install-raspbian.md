## Install Raspbian
* https://www.raspberrypi.org/downloads/raspbian/
* https://www.balena.io/etcher/

Install [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) using [Etcher](https://www.balena.io/etcher/)

Create a file called `ssh` and copy the file to the `ROOT` partition on the SD card

Reboot

`ssh pi@<PI_IP_ADDRESS>`

Then:

```sh
    sudo apt-get update
    sudo apt-get upgrade
```

Use `sudo raspi-config` to change:
* Password
* Memory Split - set Graphics to 16Mb
* Set wait for network on boot
* Change hostname if wanted

To auto setup a wifi connection (client) on boot see [Auto connect wifi](./doc/pi-zero/auto_connect_wifi.md)
