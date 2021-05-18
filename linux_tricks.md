## Linux tricks

- change title in a terminal

  ```
  echo -e '\033]2;Some Title\007'
  ```

  (see [this stackexchange entry](https://unix.stackexchange.com/a/358986))


- Direct ethernet connection between laptops

  - Issue is that you don't have DNS

  - Open Network preferences and create a Wired profile that just has,
    under IPv4, IP `192.168.0.1` on one computer and `192.168.0.2` on
    the other. Use Netmask `255.255.255.0` on both.

  - Should then be able to `scp` between them.

  - Main problem I had is that the cable I was using was bad; switched
    cables and it worked.

- Gnome extensions give error: try restarting `gnome-shell`

  ```shell
  killall -3 gnome-shell
  ```

- I have a Jabra Evolve2 40 usb headset; have had some trouble having
  it shown up as both input and output

  Solution seems to be to run `pavucontrol` and
  in the configuration tab under "Jabra Evolve2 40", select
  "Digital Stereo output + multichannel input"

  If it doesn't show up there, unplug and replug the headset.
  Sometimes it shows up as just an input, and then after that it seems
  stuck that way. Sometimes I need to plug/unplug several times before
  all of the options show up.

  It also seems like the volume is too low with "digital stereo
  output" and that it works better with "Analog stereo output"
