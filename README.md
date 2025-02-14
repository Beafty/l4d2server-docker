# l4d2server-docker-deskhub(for addons and cfg)

## Usage

First, prepare the `server.cfg` file, `host.txt` file and `motd.txt` file.

The `addons` folder is used to store mods and plugins and can be empty.
The `cfg` folder is used to store sercer.cfg and other things.

Run the container by using Docker Compose.

Notice! This is just an example, you should change the path to your own in `volumes`.

```yml
version: "3"
services:
  l4d2server:
    command: "-secure +exec server.cfg +map c1m1_hotel -port 27015"
    container_name: l4d2server
    image: beafty/l4d2_beafty:edge
    # image: ghcr.io/hoshinorei/l4d2server:edge (Where I forked from)
    ports:
      - 27015:27015
      - 27015:27015/udp
    # You can also use "host" network mode to improve little network performance.
    # network_mode: host
    restart: unless-stopped
    stdin_open: true
    tty: true
    volumes:
      - ./addons/:/home/steam/l4d2server/left4dead2/addons/
      - ./cfg:/home/steam/l4d2server/left4dead2/cfg:rw
      - ./host.txt:/home/steam/l4d2server/left4dead2/host.txt:rw
      - ./motd.txt:/home/steam/l4d2server/left4dead2/motd.txt:rw
```

```bash
cd <your docker-file-path>
docker-compose up -d
```

Enter the game server console.

```bash
docker attach l4d2server
```
