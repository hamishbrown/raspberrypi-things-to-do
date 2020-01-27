## Install a Plex server
* https://pimylifeup.com/raspberry-pi-plex-server/

Install dependencies:
```
sudo apt-get install apt-transport-https

curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -

echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list

sudo apt-get update

sudo apt-get install plexmediaserver
```

Then
```
sudo nano /etc/default/plexmediaserver
```
Replace ```export PLEX_MEDIA_SERVER_USER=plex```
with
```
export PLEX_MEDIA_SERVER_USER=pi
```

Then
```
sudo systemctl restart plexmediaserver
```

Then browse to:
```
raspberrypi.local:32400/web/
```
