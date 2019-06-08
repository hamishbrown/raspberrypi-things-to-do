## Keep your data private and secure in NextCloud*
* https://ownyourbits.com/2017/11/15/nextcloudpi-dockers-for-x86-and-arm/
* https://hub.docker.com/r/ownyourbits/nextcloudpi
* https://nextcloud.com/

Create `docker-compose.yml`

```yaml
version: '3'
services:
  nextcloudpi:
    image: ownyourbits/nextcloudpi-armhf
    command: "${IP}"
    ports:
     - "4480:80"
     - "4483:443"
     - "4443:4443"
    volumes:
     - ncdata:/data
     - /etc/localtime:/etc/localtime:ro
    container_name: nextcloudpi

volumes:
  ncdata:
```
Then
```
      IP="<PI_IP_ADDRESS" docker-compose up
```
Access at
```
        <https://<PI_IP_ADDRESS>/
```
*Requires [docker-compose](./doc/install-docker-compose.md)
