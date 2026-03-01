# WIP

Currently works as intended but is very much a WIP

Docker container for https://github.com/dazedcat19/FMD2

## Descriptions

Dockerized FMD2 (Windows with Wine) using VNC, noVNC and webSocketify to display GUI on a webpage.

https://hub.docker.com/r/docker/ablizno/fmd2

Make sure to configure it using the 'web' ui.

## Features:
* Does not require any display, works headless
* Keeps all of FMD2 features
* Since it's docker, it works on Linux
* Make use of Linuxserver ubuntu image

## Docker
```yaml
services:
  fmd2:
    image: ablizno/fmd2:latest
    container_name: fmd2
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
      - UMASK=022
      - THRESHOLD_MINUTES=3
      - TRANSFER_FILE_TYPE=.cbz
    ports:
      - 3000:3000
    volumes:
      - ./fmd:/app/FMD2/userdata
      - ./manga:/downloads
      #Needed for Flaresolverr to work
      - ./websitebypass_config.json:/app/FMD2/lua/websitebypass/websitebypass_config.json
    restart: unless-stopped
```
## Flaresolverr

In order for Flaresolverr to work, you must have the Flaresolverr container and FMD2 on the same network.
Create a file named `websitebypass_config.json` with the following contents:

```json
{
    "use_webdriver": true,
    "debug": false,
    "flaresolverr_port": 8191,
    "testing": false,
    "flaresolverr_ip": "flaresolverr"
}
```
This must be passed to the container via the compose file.

## License
[MIT](https://choosealicense.com/licenses/mit/)
