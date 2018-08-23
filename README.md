# Minecraft Server Startup Script
A basic startup script for minecraft-server

## Prerequisites

* This script has been tested on Amazon Linux AMI but should work on any Red Hat Enterprise Linux (RHEL) distro, eg: CentOS
* You should have minecraft-server installed in `WORKDIR` (default: `/usr/local/minecraft-server`)

#### Installing Minecraft Server
[TODO]

See [https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server#Linux_instructions](https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server#Linux_instructions)

#### Upgrading Minecraft Server
Assuming you already have Minecraft Server installed, you can easily upgrade to a new version like so:

```bash
wget https://launcher.mojang.com/mc/game/X.YY.Z/server/abcdefg12345/server.jar -O /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar
chown minecraft-server.daemon /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar
ln -sf /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar server.jar
service minecraft-server restart
```

## Startup Script Installation

1. Simply drop the [`minecraft-server`](minecraft-server) file into `/etc/init.d`
2. Adjust the following variables at the top of the file to match your system's capabilities:
    1. `WORKDIR` - path where minecraft-server is installed
    2. `MIN_MEMORY_ALLOCATION` - Initial memory allocation pool for JVM
    3. `MAX_MEMORY_ALLOCATION` - Maximum memory allocation pool for JVM

## Usage

* Start Minecraft Server: `service minecraft-server start`
* Stop Minecraft Server: `service minecraft-server stop`
* Restart Minecraft Server: `service minecraft-server restart`
* Get Minecraft Server Status: `service minecraft-server status`

## Notes

* The service will start in the background and ignore the HUP signal.
* stderr/stdout will be routed to `$WORKDIR/service.log`
