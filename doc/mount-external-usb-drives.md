## Mount External USB Drives

Install dependencies:
```
sudo apt-get update && sudo apt-get -y install ntfs-3g hfsutils hfsprogs acl exfat-utils hfsplus gdisk
```

Setup mount points:
```
sudo blkid

sudo mkdir /media/<DRIVE_LABEL>

sudo chmod -R 775 /media/<DRIVE_LABEL>

sudo setfacl -Rdm g:pi:rwx /media/<DRIVE_LABEL>

```

Then edit ```sudo nano /etc/fstab/```

Add similar to:

For vfat:
```
UUID=1A06-0638    /media/PACKARDBELL    vfat   nofail,uid=pi,gid=pi    0   0
```
For ext4:
```
UUID=c63a0385-3e6b-4245-88d0-a9146063484a  /media/SAMSUNG  ext4   nofail,defaults    0   0
```
For hfsplus:
```
UUID=7c9b13e1-210a-31f5-bb1b-d592b117ea6c  /media/LACIE  hfsplus  nofail,defaults    0   0
```
Using PARTUUID:
```
PARTUUID=f93fbd25-01   /media/FREECOM   vfat   nofail,uid=pi,gid=pi    0   0
```

To test:
```
sudo mount -a
```
