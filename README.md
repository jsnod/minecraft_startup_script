# Minecraft Server Startup Script
A basic startup script for minecraft-server

## Assumptions

* You already have minecraft-server installed in `WORKDIR` (default: `/usr/local/minecraft-server`)

## Installation

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

## Help

See [https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server](https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server)