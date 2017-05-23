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

### Ruby

- Ruby 2.1.5 installed on the pi, but I want 2.4.1

- Install rvm (see
  [this post](http://rayhightower.com/blog/2012/12/03/ruby-on-raspberry-pi/))

  ```
  curl -L https://get.rvm.io | bash -s stable --ruby
  ```

- He also recommends `scrot` for screenshots (`sudo apt-get install
  scrot`)

  ```
  scrot ~/desktop.png
  sleep 5; scrot ~/desktop.png
  ```

### Setting up wifi

- I think I can connect to the raspberry pi directly with an ethernet
  cable, if I need to re-set the wifi

- Looking in `/etc/network/interfaces`, it points to
  `/etc/wpa_supplicant/wpa_supplicant.conf` which has the key details

  ```
  network={
      ssid="[SSID]"
      psk="[password]"
      key_mgmt=WPA-PSK
  }
  ```

### MongoDB

See
<http://yannickloriot.com/2016/04/install-mongodb-and-node-js-on-a-raspberry-pi/>

```
sudo apt-get install mongodb-server
sudo pip3 install pymongo
```

For some reason, `mongod` gives an error about the standard port
27017, being used. But if we use `--port 27016`, that's okay.

```
sudo mkdir /data
sudo mkdir /data/db
sudo chown -R pi /data
mongod --port 27016
```

### Node

See <https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions>

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install -y build-essential
```

Also to get coffeescript, `sudo npm install -g coffee-script
