## Host your own Apache simple HTML website*
* https://httpd.apache.org/
* https://hub.docker.com/_/httpd
---
Create a directory for your website files called `public-html`

        mkdir public-html

Copy your website files (.html, .js, .css) into `public-html`

Create `Dockerfile`

        nano Dockerfile

Copy and Paste the following code

        FROM httpd:2.4
        COPY ./public-html/ /usr/local/apache2/htdocs/

Save and Exit the file

        <Ctrl-x>y<Enter>

Build `<YOUR_IMAGE_NAME>`

        docker build -t <YOUR_IMAGE_NAME> .

Run `<YOUR_CONTAINER_NAME>`

        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>

Access at

        <http://<PI_IP_ADDR>/<YOUR_WEB_SITE_PAGE>
---
*Requires [Docker](./install-docker.md)
