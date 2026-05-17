# pi-hole

Ad blocker on raspberry pi. I'm using a raspberry pi 4 with 1 GB RAM

## Resources

- [pi-hole github](https://github.com/pi-hole/pi-hole)

- [running pi-hole on a raspberry
  pi](https://www.raspberrypi.com/tutorials/running-pi-hole-on-a-raspberry-pi/)

- [the beauty of having a pi-hole](https://den.dev/blog/pihole/)

## Installation

- Write raspi software to SD card

  - raspberry pi OS lite (64-bit)
  - host `pihole`
  - enable ssh

- Start up and log in to raspberry pi

- Install some stuff

  - `sudo apt update`
  - `sudo apt upgrade`
  - neofetch from [github](https://github.com/dylanaraps/neofetch)
    - `wget https://github.com/dylanaraps/neofetch/archive/refs/tags/7.1.0.tar.gz`
    - `tar xzvf 7.1.0.tar.gz`
    - `cd neofetch-7.1.0`
    - `sudo make install`
  - `sudo apt install mg`
  - `sudo apt install git`

- Set up ssh key
  - `ssh-keygen -t ed25519 -C "<email>"`
  - ssh-agent or keychain

- Install tmux
  - `wget https://github.com/tmux/tmux/releases/download/3.6a/tmux-3.6a.tar.gz`
  - `sudo apt install libevent-dev libncurses-dev build-essential bison pkg-config`
  - `tar xzvf tmux-3.6a.tar.gz`
  - `cd tmux-3.6a
  - `./configure && make`
  - `sudo make install`
  - copy `.tmux.conf` from laptop

- Create static IP for the pihole

  - determine MAC address with `ifconfig -a`
  - log in to router and go to LAN -> DHCP
  - reboot to hopefully have it get the new IP
  - that didn't work, so tried the [instructions here](https://www.abelectronics.co.uk/kb/article/31/set-a-static-ip-address-on-raspberry-pi-os-trixie)
    using a bunch of `nmcli` commands

- Install pi-hole from instructions in its [README](https://github.com/pi-hole/pi-hole)
  - using google DNS, logging queries, and privacy level "show everything"
  - write down admin webpage and login
  - configure router to have DHCP clients use pi-hole as DNS server


---

Tried installing [nagios](nagios.md) on top of [pihole](pihole.md) on
the same raspberry pi and they stepped on top of each other.
Both are using apache2 server. Instead installed nagios on
the raspberry pi that I'm using as a minecraft server
