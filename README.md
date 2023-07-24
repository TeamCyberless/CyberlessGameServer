[![Docker Pulls](https://img.shields.io/docker/pulls/teamcyberless/cyberlessonlineserver.svg)](https://hub.docker.com/r/teamcyberless/cyberlessonlineserver)
[![Image Size](https://img.shields.io/docker/image-size/teamcyberless/cyberlessonlineserver/latest.svg)](https://hub.docker.com/r/teamcyberless/cyberlessonlineserver)

| [**English**](https://github.com/TeamCyberless/CyberlessGameServer/blob/master/README.md) | [Turkish](https://github.com/TeamCyberless/CyberlessGameServer/blob/master/README-tr.md) |
| ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |

# Cyberless: Online Game Server

Cyberless: Online is online TPS shooter character-based game. This repository contains only Linux server for now.

For detailed information about Cyberless: Online, visit [here](https://store.steampowered.com/app/1175540/Cyberless_Online/) or send us [e-mail](mailto:teamcyberless@gmail.com).

## Tags

*   [`latest`](dockerfiles/latest/Dockerfile)

## Usage

### Pull latest image
```shell
docker pull teamcyberless/cyberlessonlineserver:latest
```

### Test interactively
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it teamcyberless/cyberlessonlineserver:latest
```

### Test with some game server parameters
```
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it teamcyberless/cyberlessonlineserver:latest \
  ./CyberlessOnline/Binaries/Linux/CyberlessOnlineServer-Linux-Shipping \
  /Game/Maps/Training?ServerPassword=passwd?TimeLimit=20?GoalScore=330 \
  -server -log -Messaging -SteamServerName="My Server"
```

### Run with volume (You must first create a volume)
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it \
  --user cyberless \
  --mount source=<volume name>,target=/opt/CyberlessOnlineServer \
  teamcyberless/cyberlessonlineserver:latest
```

### All Together
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it \
  --user cyberless \
  --mount source=<volume name>,target=/opt/CyberlessOnlineServer \
  teamcyberless/cyberlessonlineserver:latest \
  ./CyberlessOnline/Binaries/Linux/CyberlessOnlineServer-Linux-Shipping \
  /Game/Maps/Training?ServerPassword=passwd?TimeLimit=20?GoalScore=330 \
  -server -log -Messaging -SteamServerName="My Server"
```

## Used Ports

* 7777 (TCP/UDP)
* 27015 (TCP/UDP)

## Some Commonly Used Parameters

| **Parameter Name** | **Type** | **Is Level Parameter** | **Description**                                                                   | **Default Value** |
| ------------------ | :------: | :--------------------: | --------------------------------------------------------------------------------- | :---------------: |
| ServerPassword     |  string  |           ✔️            | The password will be asked while login to server (empty value means no password). |     *(empty)*     |
| TimeLimit          | integer  |           ✔️            | Match maximum playable time without overtime (0 means infinite time).             |  15 *(minutes)*   |
| GoalScore          | integer  |           ✔️            | Goal score of player scores or team scores (0 means no goal score).               |        300        |
| -LAN               |   bool   |           ❌            | Starts game server as local server                                                |  *(not passed)*   |
| -SteamServerName   |  string  |           ❌            | Sets Steam server name                                                            |  *(not passed)*   |
