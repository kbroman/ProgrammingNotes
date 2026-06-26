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

  Now it's giving me a different set of options; going to try
  stereo output + mono input. In zoom, the headset has been really
  quiet.

- Regarding disk encryption passwords on system76: See
  [disk encryption passwords](https://support.system76.com/articles/advanced-luks/
  and
  [Change LUKS passphrase](https://support.system76.com/articles/password/#changing-luks-passphrase)

  ```
  lsblk -f

  sudo cryptsetup luksDump /dev/sda3
  sudo cryptsetup luksAddKey /dev/sda3
  sudo cryptsetup luksChangeKey /dev/sda3 -S 0
  ```

- Figure out what to install to get a particular command: `apt-file`:

  ```shell
  sudo apt install apt-file
  sudo apt-file update

  # determine what to install to get ip command:
  apt-file search --regexp 'bin/ip$'

  # (the answer is iproute2)
  ```

- For controlling settings of logitech mice (such as my M720), see [logiops](https://github.com/PixlOne/logiops)
  See also <https://medium.com/@jeromedecinco/configuring-logiops-for-logitech-mx-master-3s-on-rhel-based-systems-d3971101c324>

  ```shell
  sudo apt install logiops
  sudo logid
  ```

- recursive chmod, separately for directories and files:

  ```shell
  find . -type d -exec chmod 755 {} \;
  find . -type f -exec chmod 644 {} \;
  ```
