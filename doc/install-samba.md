## Install SAMBA to share drives across your local networks
* https://pimylifeup.com/raspberry-pi-samba/

Install dependencies:
```
sudo apt-get install samba samba-common-bin
```

Edit smb.conf:
```
sudo nano /etc/samba/smb.conf
```

Add similar to:
```
[SAMSUNG] #This is the name of the share it will show up as when you browse
comment = SAMSUNG 2.7T
path = /media/SAMSUNG
create mask = 0775
directory mask = 0775
read only = no
browseable = yes
public = yes
force user = pi
#force user = root
only guest = no
```

Add SAMBA user pi:
```
sudo smbpasswd -a pi
```

Restart SAMBA service:
```
sudo systemctl restart smbd
```
