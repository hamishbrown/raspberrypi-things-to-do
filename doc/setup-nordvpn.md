## Setup NordVPN using OpenVPN
* https://zone13.io/post/raspberry-pi-vpn-gateway-for-nordvpn/
* https://support.nordvpn.com/Connectivity/Linux/1047409422/Connect-to-NordVPN-using-Linux-Terminal.htm
* https://support.nordvpn.com/General-info/1047409702/What-are-your-DNS-server-addresses.htm

```
sudo nano /etc/network/interfaces
```
Add the following lines
```
auto eth0
    iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
```
Install necessary packages
```
sudo apt install openvpn iptables-persistent python3-requests -y
```
NordVPN setup
```
cd /etc/openvpn

sudo su

wget https://downloads.nordcdn.com/configs/archives/servers/ovpn.zip

unzip ovpn.zip

cp ovpn_udp/*.ovpn .

rm -rf ovpn_tcp ovpn_udp
```
Continue as su
```
nano login.txt
```
Add the following lines, see https://support.nordvpn.com/Connectivity/Linux/1047409422/Connect-to-NordVPN-using-Linux-Terminal.htm
```
_Your_NordVpn_Username_
_Your_NordVpn_Password_
```
Update config files
```
sed -i 's/auth-user-pass/auth-user-pass login.txt/' *.ovpn
```
Exit su
```
exit
```
```
mkdir /home/pi/vpn
cd /home/pi/vpn
```
Create connector.py script
```
nano connector.py
````
Add the following lines
```
#!/usr/bin/env python

import os
import json
import subprocess
import time
import requests

os.chdir("/etc/openvpn")

# Command to kill any running instances of OpenVPN
kill_command = "sudo killall openvpn"

# URL to the NordVPN server connection tool obtained from the browser
url = 'https://nordvpn.com/wp-admin/admin-ajax.php?action=servers_recommendations&filters={%22country_id%22:227}' # Insert URL here

def start_openvpn_connection():
    response = requests.get(url)

    if len(response.text) != 2:
        nvpn_response = json.loads(response.text)
        vpn_info = nvpn_response[0]
        vpn_info_hostname = vpn_info["hostname"]
        vpn_file = vpn_info_hostname + ".udp.ovpn"

        # Command to start Openvpn
        ov_command = "sudo openvpn --config " + vpn_file

        # Start the NordVPN connection
        subprocess.Popen(ov_command.split())

if __name__ == "__main__":
    subprocess.Popen(kill_command.split())
    time.sleep(2)
    start_openvpn_connection()
```
```
sudo nano /etc/rc.local
```
Add following line before ```exit 0```
```
python /home/pi/vpn/connector.py
```
Install ```nslookup```
```
sudo apt-get install dnsutils -y
```
Find NordVPN servers
```
nslookup nordvpn.com
```
Use IP addresses in the following script
```
nano setup-iptables.sh
```
```
#!/bin/bash
sudo iptables -F
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT

sudo iptables -t nat -A POSTROUTING -o tun0 -j MASQUERADE
sudo iptables -A FORWARD -i tun0 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o tun0 -j ACCEPT

sudo iptables -A OUTPUT -o tun0 -m comment --comment "vpn" -j ACCEPT
sudo iptables -A OUTPUT -o eth0 -p icmp -m comment --comment "icmp" -j ACCEPT
sudo iptables -A OUTPUT -d 192.168.1.0/24 -o eth0 -m comment --comment "lan" -j ACCEPT
sudo iptables -A OUTPUT -o eth0 -p udp -m udp --dport 1194 -m comment --comment "allow vpn traffic" -j ACCEPT
sudo iptables -A OUTPUT -o eth0 -p udp -m udp --dport 123 -m comment --comment "ntp" -j ACCEPT
sudo iptables -A OUTPUT -p tcp -d 104.17.49.74 --dport 443 -m comment --comment "nordvpn IP" -j ACCEPT
sudo iptables -A OUTPUT -p tcp -d 104.17.50.74 --dport 443 -m comment --comment "nordvpn IP" -j ACCEPT
sudo iptables -A OUTPUT -o eth0 -j DROP
sudo iptables -I FORWARD -i eth0 ! -o tun0 -j DROP

sudo iptables-save | sudo tee /etc/iptables/rules.v4
```
Make it executable
```
chmod +x setup-iptables.sh
```
Edit ```hosts``` file
```
sudo nano /etc/hosts
```
Add NordVPN servers
```
104.17.49.74  nordvpn.com
104.17.50.74  nordvpn.com
```
Set up IP forwarding
```
sudo nano /etc/sysctl.conf
```
Uncomment following line
```
net.ipv4.ip_forward=1
```
Run the following command to enable the changes
```
sudo sysctl -p /etc/sysctl.conf
```
Run ```setup-iptables.sh```
```
./setup-itables.sh
```
Reboot Pi

Point your Gateway to this Pi's IP address to use VPN

Use NordVPN DNS servers on your router
```
103.86.96.100
103.86.99.100
```