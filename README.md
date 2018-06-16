# Minecraft Server Startup Script
A basic startup script for minecraft-server

## Assumptions

* You already have minecraft-server installed in `/usr/local/minecraft-server`

## Installation

1. Simply drop the [`minecraft-server`](minecraft-server) file into `/etc/init.d`
2. Adjust the `-Xms` and `-Xmx` in the `start()` function to match your system's capabilities

## Notes

* The service will start in the background and ignore the HUP signal.
* stderr/stdout will be routed to `$WORKDIR/service.log`

## Help

See [https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server](https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server)