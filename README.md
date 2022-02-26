# Docker.X11
Getting large X11 programs to run in Docker


## Gimp in Docker

docker run \
  --rm \
  -i \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v gimp-git-data:/export:ro \
  -v gimp-bin:/data \
  gimp:latest \
    /bin/bash -c 'tar -C "$PREFIX" -xzf /data/gimp-internal.tar.gz && gimp'

## LibreOffice in Docker

docker run \
  -d \
  --name=libreoffice \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -p 3000:3000 \
  -v /tmp/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/libreoffice



