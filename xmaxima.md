This is still a work in progress.  Has not been tested.

## Start a container in the background
```bash
docker run \
  --rm \
  -it \
  --env "DISPLAY=${DISPLAY}" \
  --hostname ${HOSTNAME} \
  --volume "${HOME}/.Xauthority:/root/.Xauthority:rw" \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume "${PWD}":/tmp/maxima/ \
  --workdir /tmp/maxima/ \
  --user root \
  --env "HOME=/root" \
  --name maxima \
  ubuntu \
  sleep inf &
```

## Install the software
```bash
docker container exec -i maxima <<'eof'
  export DEBIAN_FRONTEND=noninteractive
  apt-get update
  apt-get install -y xmaxima
eof
```

## Run xmaxima
```bash
docker container exec maxima xmaxima
```


