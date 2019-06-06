## Install Portainer*
* https://www.portainer.io/
* https://hub.docker.com/r/portainer/portainer/
---
        docker run -d -p 9000:9000 \
            -v /var/run/docker.sock:/var/run/docker.sock \
            -v portainer_data:/data \
            portainer/portainer
---
*Requires [Docker](./install-docker.md)
