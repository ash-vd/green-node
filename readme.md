# Green node (Docker)

Runs the Green node software (Connect United, v2.6.1-b, linux/amd64) in a Docker container.
Mirrors the setup in `../element-node`.

## Download the node binary

The binary is not committed yet. Fetch it from Green's download server
(the same server their official Linux installer, `linux.sh`, uses):

```
mkdir -p bin
curl -fL -o bin/green-node_linux-amd64 \
  https://download.setpowerfree.com/node-binaries/v2.6.1-b/green-v2.6.1-b_linux-amd64
```

Expected size: 6,874,384 bytes.

## Set your credentials

```
cp login.env.example login.env
```

Open `login.env` and replace `email@domain.com` and `password` with your Green account login.

## Create the image

```
docker build . -t green-node
```

> For each node that you want to set up, run the following commands. Increment the number for each successive node
> (green-node-volume1, green-node-volume2, ...). Make sure the number matches in both commands.

## Create a volume to store your config file

```
docker volume create green-node-volume1
```

## Run this once to create a container

Afterwards, you can see it in Docker Desktop and restart it from there if needed.

```
docker run --name green-node1 -d -v green-node-volume1:/root --restart unless-stopped --env-file login.env green-node
```

Check it with `docker logs -f green-node1` and the `version` command:

```
docker run --rm green-node /usr/local/bin/green-node_linux-amd64 version
```
