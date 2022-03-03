# GoAccess for Nginx Proxy Manager Logs

Still in development... You might need to wait a bit if you have a large amount of logs for it to parse.

Docker image: https://hub.docker.com/r/xavierh/goaccess-for-nginxproxymanager

Docker tags: https://hub.docker.com/r/xavierh/goaccess-for-nginxproxymanager/tags

Github Repo: https://github.com/xavier-hernandez/goaccess-for-nginxproxymanager

<br>

![Alt text](https://i.ibb.co/fNj9Dcy/goaccess1.jpg "GoAccess Dashboard")

New to creating docker images so bear with me. I did this more for me then for public consumption but it appears to work so maybe someone might find it useful.

This docker container should work out of the box with Nginx Proxy Manager to parse proxy logs. The goaccess.conf has been configured to only access proxy logs and archived proxy logs.

The docker image scans and includes files matching the following criteria: proxy-host-*_access.log.gz proxy-host-*_access.log

Currently using GoAccess version: 1.5.5

<br>

---
## Choose your version 

**stable:** xavierh/goaccess-for-nginxproxymanager:latest

**latest stable development:** xavierh/goaccess-for-nginxproxymanager:develop

Thanks to Just5KY you can find the arm version here: [justsky/goaccess-for-nginxproxymanager](https://hub.docker.com/r/justsky/goaccess-for-nginxproxymanager)

---

<br>

```yml
goaccess:
    image: xavierh/goaccess-for-nginxproxymanager:latest
    container_name: goaccess
    restart: always
    environment:
        - TZ=America/New_York
    ports:
        - '7880:7880'
    volumes:
        - /path/to/host/nginx/logs:/opt/log
```
If you have permission issues, you can add PUID and PGID with the correct user id that has read access to the log files.
```yml
goaccess:
    image: xavierh/goaccess-for-nginxproxymanager:latest
    container_name: goaccess
    restart: always
    volumes:
        - /path/to/host/nginx/logs:/opt/log
    ports:
        - '7880:7880'
    environment:
        - PUID=0
        - PGID=0
        - TZ=America/New_York        
```
docker run for pi-hosted setups
[12:19 AM]
sudo docker run -d \
   --name=goaccess \
   -e PUID=1000 \
   -e PGID=1000 \
   -e TZ=America/Chicago \
   -v /portainer/Files/AppData/Config/nginx-proxy-manager/data:/opt/log \
   -p 7880:7880 \
   --restart unless-stopped \
   justsky/goaccess-for-nginxproxymanager
   ...

Thanks to https://github.com/GregYankovoy for the inspiration, and for their nginx.conf :)

This product includes GeoLite2 data created by MaxMind, available from
<a href="https://www.maxmind.com">https://www.maxmind.com</a>.
