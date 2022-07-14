## Debian

- Had a dns problem; this seemed to work temporarily

  ```
  sudo dhclient -r
  sudo dhclient eth0
  ```

- I'm using debian on an old laptop, on which I've installed
  a minecraft server (using [spigot](https://www.spigotmc.org)).

  Basic instructions at [here](https://lemire.me/blog/2016/04/02/setting-up-a-robust-minecraft-server-on-a-raspberry-pi/)

- I'm using screen to switch between having the server in the
  foreground vs background.

  - `screen -list` to list running jobs.
  - `screen -r` to bring the minecraft server to the foreground
  - `ctrl-a d` to put it back in the background
