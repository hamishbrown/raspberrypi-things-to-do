## Auto Configure Wifi connection on boot
* Mount SD card on external PC
* Create file `wpa_supplicant.conf` in `boot` partition
```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
	ssid="MyWiFiNetwork"
	psk="aVeryStrongPassword"
	key_mgmt=WPA-PSK
}
```
