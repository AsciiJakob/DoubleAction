# Double Action: Boogaloo Dedicated Server

The follwing docker image allows for running a Double Action: Boogaloo dedicated server

*This is a fork improving on [GameServers/DoubleAction](https://github.com/GameServers/DoubleAction). Credit goes to them for the shell scripts and base Dockerfiles. This fork adds various new ENV variables and fixes an issue where the server config would not apply itself.

[The GitHub repo for this image.](https://github.com/AsciiJakob/DoubleAction)

Container Runtime Environment Variables:

* APP_SERVER_PORT 		- Port for the game to run on (default 27015)
* APP_SERVER_MAXPLAYERS 	- Max number of players (default 10). This is capped to 16 by the game.
* APP_SERVER_MAP 		- Starting map (default da_cocaine)
* APP_SERVER_NAME		- The Name of the server
* APP_SERVER_BOTS		- Number of bots (default 4)
* APP_SERVER_PASSWORD		- The password for the server (default none/disabled)
* APP_RCON_PASSWORD        	- RCON password for the server (default none/disabled)
* APP_SERVER_TOKEN		- Use access token from [http://steamcommunity.com/dev/managegameservers](http://steamcommunity.com/dev/managegameservers)

# Example usage:
docker-compose.yml:
```
version: '3.7'

services:
  doubleActionServer:
    image: asciijakob/doubleaction:latest
    environment:
      APP_SERVER_PORT: 27015
      APP_SERVER_MAXPLAYERS: 24
      APP_SERVER_MAP: da_cocaine
      # You can get your access token from the link above this example.
      APP_SERVER_TOKEN: replaceMe
      APP_SERVER_NAME: "Server name"
      APP_SERVER_BOTS: 0
    ports:
      - 27015:27015
      - 27015:27015/udp
```
If you would like to add your own server.cfg, append the following to the bottom of your docker-compose.yml and have a server.cfg present in the same directory as your docker-compose file. Although, please keep in mind that the environment variables will override all the settings it controls and ignore whatever value it has in the server.cfg.
```
    volumes:
      - ./server.cfg:/tmp/server.cfg
```
For the default server.cfg, see [server.cfg](https://github.com/AsciiJakob/DoubleAction/blob/master/server.cfg)
