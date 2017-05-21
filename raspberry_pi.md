## Raspberry Pi

### Set up

- Needed to switch keyboard to generic 101 PC _US_ (default was _UK_
  and had `@` and `"` switched)

- Enable ssh: in X windows, click raspberry on menu bar → Preferences
  → raspberry pi configuration → interfaces (this is also in the raspi-config 
  menu, within "interfaces".


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
  ``
