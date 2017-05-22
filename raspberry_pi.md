## Raspberry Pi

### Set up

- Use
  [full Raspbian](https://www.raspberrypi.org/downloads/raspbian/); to
  get on SD card, use [Etcher](https://etcher.io/).

- `sudo raspi-config`:

  - change password
  - change host name
  - expand file system to use full SD card
  - boot to shell
  - configure time zone and locale (US english)
  - keyboard to Generic 101 PC / US (default is _UK_ and has `@` and
    `"` switched)
  - enable ssh (under "interfaces")


### Basic things

- Restart and stop: `sudo reboot` and `sudo halt`

- `apt-get update`


### Minecraft


- [Setting up a robust minecraft server](http://lemire.me/blog/2016/04/02/setting-up-a-robust-minecraft-server-on-a-raspberry-pi/)

- Minecraft server is [spigot](https://www.spigotmc.org)

- You can install minecraft 1.9 rather than the latest version
  (currently 1.11.2). See
  [this tutorial](https://www.epiphanydigest.com/2016/03/07/learn-to-program-with-minecraft-on-ubuntu/)
  or
  [this one](http://simplyrisc.blogspot.co.uk/2016/03/learn-to-program-with-minecraft-on.html)

  ```
  git config --global --unset core.autocrlf
  java -jar BuildTools.jar --rev 1.9
  ```

  Ultimately I was able to use the latest one.

- Key commands:

  ```
  wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
  java -jar BuildTools.jar
  java -jar -Xms512M -Xmx1008M spigot-1.11.2.jar nogui
  ```

- Put [RaspberryJuice](https://dev.bukkit.org/projects/raspberryjuice) in `minecraft/plugins/`

- Edit `server.properties`

  ```
  gamemode=1
  force-gamemode=true
  max-players=6
  view-distance=8
  ```
