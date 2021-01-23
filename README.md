# Minecraft Server Startup Script
A basic startup script for minecraft-server

## Prerequisites

* This script has been tested on Amazon Linux AMI but should work on any Red Hat Enterprise Linux (RHEL) compatible distro, eg: CentOS
* You should have minecraft-server installed in `WORKDIR` (default: `/usr/local/minecraft-server`)

## Installation

1. Simply drop the [`minecraft-server`](minecraft-server) file into `/etc/init.d`
2. Adjust the following variables at the top of the file to match your system's capabilities:
    1. `WORKDIR` - path where minecraft-server is installed
    2. `MIN_MEMORY_ALLOCATION` - Initial memory allocation pool for JVM
    3. `MAX_MEMORY_ALLOCATION` - Maximum memory allocation pool for JVM
    4. `JAVA_FLAGS` - By default this script uses Java flags recommended by [Aikar](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/).  Adjust as needed for your system.

## Usage

* Start Minecraft Server: `service minecraft-server start`
* Stop Minecraft Server: `service minecraft-server stop`
* Restart Minecraft Server: `service minecraft-server restart`
* Get Minecraft Server Status: `service minecraft-server status`

## Notes

* The service will start in the background and ignore the HUP signal.
* stderr/stdout will be routed to `$WORKDIR/service.log`

## Help

#### Installing Minecraft Server
[TODO]

See [https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server#Linux_instructions](https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server#Linux_instructions)

#### Upgrading Minecraft Server
Assuming you already have Minecraft Server installed, you can easily upgrade to a new version like so:

```bash
wget https://launcher.mojang.com/mc/game/X.YY.Z/server/abcdefg12345/server.jar -O /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar
chown minecraft-server.daemon /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar
ln -sf /usr/local/minecraft-server/minecraft_server.X.YY.Z.jar /usr/local/minecraft-server/server.jar
service minecraft-server restart
```

#### Checking Server Logs
```bash
sudo tail --lines=500 -f /usr/local/minecraft-server/logs/latest.log
```

#### Making Your Server Private
1. Edit `/usr/local/minecraft-server/server.properties` and set enforcement of whitelist:
    ```
    enforce-whitelist=true
    ```
2. Restart the server: `service minecraft-server restart`

#### Adding Users To Your Private Server
1. Find the user's UUID from one of these sites:
    * [namemc.com](https://namemc.com/)
    * [mcuuid.net](https://mcuuid.net/)
2. Edit `/usr/local/minecraft-server/whitelist.json` and add them:
    ```javascript
    [
      {
        "uuid": "d56f5713-fb33-4b2c-ab22-725cb362542d",
        "name": "SomeUser"
      },
      {
        "uuid": "034b1c1c-4a1c-463b-b70e-1c0c53737efd",
        "name": "AnotherUser"
      },
    ]
    ```
    * The `name` attribute is freeform, not the actual username, so make it descriptive so that you know who it is! Users can change their names over time so use this to know who it is.
3. Restart the server: `service minecraft-server restart`
