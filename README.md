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
```bash
docker run \
  -d \
  --name octave \
  --env "DISPLAY=$DISPLAY" \
  --volume "$HOME/.Xauthority:/root/.Xauthority:rw" \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume "${PWD}":/tmp/octave/ \
  --hostname $HOSTNAME \
  --user root \
  --env "HOME=/root" \
  --workdir /tmp/octave/ \
  --entrypoint octave \
  gnuoctave/octave:7.1.0 \
  --gui
```
