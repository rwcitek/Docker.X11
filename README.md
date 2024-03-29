# Docker with X11/Wayland
Getting large X11/Wayland programs to run in Docker on a Chromebook.


## Gimp
```bash
docker run \
  --rm \
  -i \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v gimp-git-data:/export:ro \
  -v gimp-bin:/data \
  gimp:latest \
    /bin/bash -c 'tar -C "$PREFIX" -xzf /data/gimp-internal.tar.gz && gimp'
```

## LibreOffice
```bash
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
```

## Octave
- https://hub.docker.com/r/gnuoctave/octave
```bash
docker run \
  --detach \
  --env "DISPLAY=${DISPLAY}" \
  --hostname ${HOSTNAME} \
  --volume "${HOME}/.Xauthority:/root/.Xauthority:rw" \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume "${PWD}":/tmp/octave/ \
  --workdir /tmp/octave/ \
  --user root \
  --env "HOME=/root" \
  --entrypoint octave \
  --name octave \
  gnuoctave/octave:7.1.0 \
  --gui
```

## Python Turtle, a LOGO implementation
- https://realpython.com/beginners-guide-python-turtle/
```bash
# start a docker container
docker run \
  --detach \
  --env "DISPLAY=${DISPLAY}" \
  --hostname ${HOSTNAME} \
  --volume "${HOME}/.Xauthority:/root/.Xauthority:rw" \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --name turtle \
  ubuntu:22.04 sleep inf
```
```bash
# install python
<<'eof' docker exec -i turtle bash
  export DEBIAN_FRONTEND=noninteractive
  apt-get update
  apt-get install -y python3-pip python3-tk
eof
```
```bash
# run a sample program
<<'eof' docker exec -i turtle python3
import time
import turtle
s = turtle.getscreen()
t = turtle.Turtle()

time.sleep(10)

t.speed(10)
i=40
for _ in range(i):
  for _ in range(4):
    t.right(90)
    t.forward(100)
  t.right(360/i)

time.sleep(10)
eof
```


