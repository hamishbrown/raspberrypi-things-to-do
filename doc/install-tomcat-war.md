## Host your own Tomcat webapp*
* http://tomcat.apache.org/
* https://hub.docker.com/_/tomcat

In the directory containing your WAR file
```
        nano Dockerfile
```
Copy and Paste the following code
```
        FROM tomcat:8.5
        COPY ./<YOUR_WEB_APP_NAME>.war /usr/local/tomcat/webapps/
```
Save and Exit the file
```
        <Ctrl-x>y<Enter>
```
Build `<YOUR_IMAGE_NAME>`
```
        docker build -t <YOUR_IMAGE_NAME> .
```
Run `<YOUR_CONTAINER_NAME>`
```
        docker run -dit --name <YOUR_CONTAINER_NAME> -p 8080:8080 <YOUR_IMAGE_NAME>
```
Access at
```
        http://<PI_IP_ADDR>:8080/<YOUR_WEB_APP_NAME>
```
*Requires [Docker](./install-docker.md)
