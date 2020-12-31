## Raspberry Pi

### Set up

- Downloaded and installed Raspberry Pi Imager,
  <https://www.raspberrypi.org/software/>

- Downloaded Raspberry Pi OS,
  <https://www.raspberrypi.org/software/operating-systems/>

- Wrote Raspberry Pi OS to SD card using Imager

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

Also to get coffeescript, `sudo npm install -g coffee-script`


### Network diagnostics

Cool project to make web server with local network diagnostics:
<https://pimylifeup.com/raspberry-pi-nagios/>

Also tried to use this to:
- check internet speed, <https://github.com/jonwitts/nagios-speedtest>
- check websites, <https://github.com/catinello/nagios-check-website>
- graphs, <https://blog.ruanbekker.com/blog/2019/03/18/how-to-setup-the-nagiosgraph-plugin-on-nagios-monitoring-server/>


### GPIO

See the [Adafruit lesson about GPIO with Raspberry
Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup)

- Install stuff (didn't seem necessary for me)

  ```
  sudo apt install -y python-smbus i2c-tools
  ```

- Configuration: use `sudo raspi-config` and
  go to Interfacing Options -> I2C and enable.
  Also an option for remote GPIO.
  Also enable SPI

- Test I2C

  ```
  sudo i2cdetect -y 1
  ```

- Reboot

- See also [the official
  docs](https://www.raspberrypi.org/documentation/usage/gpio/python/README.md)
  which suggests using the [GPIO
  zero](https://gpiozero.readthedocs.io/en/stable/) library:

  ```
  sudo pip3 install gpiozero
  ```

- LED: pin 20 -> long leg of LED -> resistor -> ground

  ```python
  from gpiozero import LED
  from time import sleep

  led = LED(20)

  led.on()
  sleep(1)
  led.off()
  ```

- button: pin 21 -> button; other side of button -> resistor -> ground

  ```python
  from gpiozero import Button
  from gpiozero import LED
  from time import sleep

  led = LED(20)
  button = Button(21)
  while True:
      if button.is_pressed
          led.on()
      else
          led.off()
      sleep(0.1)
  ```

- even better, with button and led:

  ```python
  from gpiozero import LED, Button
  from signal import pause

  led = LED(20)
  button = Button(21)

  button.when_pressed = led.on
  button.when_released = led.off

  pause()
  ```
