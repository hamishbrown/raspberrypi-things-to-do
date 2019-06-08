## Install Docker Registry*
* https://docs.docker.com/registry/
* https://hub.docker.com/r/joxit/docker-registry-ui/dockerfile
* https://github.com/Joxit/docker-registry-ui/tree/master/examples/ui-as-proxy/

Create `docker-compose.yml`

```yaml
version: '2'
services:
  registry:
    image: registry:2.6.2
    volumes:
      - ./registry-data:/var/lib/registry
    networks:
      - registry-ui-net

  ui:
    image: joxit/docker-registry-ui:arm32v7-static
    ports:
      - 80:80
    environment:
      - REGISTRY_TITLE=My Pi Docker Registry
      - REGISTRY_URL=http://registry:5000
    depends_on:
      - registry
    networks:
      - registry-ui-net

networks:
  registry-ui-net:
```
Start with `docker-compose up -d`

Access at
```
        http://localhost/
```
#### To populate the registry
Create `populate.sh`

```
        #!/bin/bash

        docker tag joxit/docker-registry-ui:arm32v7-static localhost/joxit/docker-registry-ui:arm32v7-static
        docker tag joxit/docker-registry-ui:arm32v7-static localhost/joxit/docker-registry-ui:0.3.0-arm32v7-static
        docker tag joxit/docker-registry-ui:arm32v7-static localhost/joxit/docker-registry-ui:0.3-arm32v7-static

        docker push localhost/joxit/docker-registry-ui

        docker tag registry:2.6.2 localhost/registry:latest
        docker tag registry:2.6.2 localhost/registry:2.6.2
        docker tag registry:2.6.2 localhost/registry:2.6
        docker tag registry:2.6.2 localhost/registry:2.6.0
        docker tag registry:2.6.2 localhost/registry:2

        docker push localhost/registry
```
Save and Exit the file
```
        <Ctrl-x>y<Enter>
```
Make it executable and run it
```
        chmod +x populate.sh
        ./populate.sh
```
*Requires [docker-compose](./doc/install-docker-compose.md)
