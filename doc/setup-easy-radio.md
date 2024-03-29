## Install Easy Radio*
* https://github.com/hamishbrown/easy-radio

Create `docker-compose.yml`

```yaml
version: "2"
services:
  radio:
    image: hamishbrown/easy-radio
    restart: unless-stopped
    environment: 
      - TZ=Europe/Dublin
      - ICECAST_PASS=hackme                   # RECOMMENDED Change in icecast.xml and update here
    ports:
      - 8000:8000
    volumes:
      - </path/to/music/folder>:/tracks:ro    # *** REQUIRED*** Update with the path to your host music folder

      # Optional volumes
      - ./icecast.xml:/radio/icecast.xml:rw   # Optional use to override icecast defaults. Recommended to change default password
      - ./live.liq:/radio/live.liq:rw         # Optional override to use your own script
      - ./icecast_logs:/var/log/icecast2:rw    # Optional map icecast logs, set liquidsoap log file in 'live.liq'
```
Start with `docker-compose up -d`

## Enjoy
Wait a few seconds depending on the number of tracks in your music folder

Open your browser at
```
http://localhost:8000/radio
```
*Requires [docker-compose](./doc/install-docker-compose.md)
