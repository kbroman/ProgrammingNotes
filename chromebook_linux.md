## Linux on a chromebook

Got an [Acer Chromebook
14](https://www.amazon.com/gp/product/0387921249?ie=UTF8&tag=7210-20)
with 1920x1080 screen, 4 GB RAM, and 32 GB SSD (says model number
CB3-431; chromeOS model `EDGAR D25-E5K-S8I-A85`)

I also bought two [Acer
C910-54M1](https://www.acer.com/ac/en/US/content/professional-model/NX.EF3AA.011):1920x1080
screen, 4 GB RAM, 32 GB SSD, and Intel i5 chips (vs. Celeron for the
Chromebook 14). The SSD can be upgraded; I used [this 128 GB
SSD](https://www.amazon.com/gp/product/B01N659X8H?ie=UTF8&tag=7210-20).
The chromeOS model numbers were slightly different: `YUNA
D25-A3G-K4A-A3L` and `YUNA D25-C3C-43I-A6F`.


### Some links

- [lifehacker](https://lifehacker.com/how-to-install-linux-on-a-chromebook-and-unlock-its-ful-509039343)
- [softpedia](http://news.softpedia.com/news/how-to-install-ubuntu-17-04-with-gnome-on-your-chromebook-alongside-chrome-os-516624.shtml)
- [Jenny Bryan](https://github.com/jennybc/operation-chromebook)

### General procedure

- Put into recovery mode (esc-refresh-power)

- ctrl-D to put in developer mode

- ctrl-alt-T to open a terminal, then type `shell` in the terminal

- download [crouton](https://github.com/dnschneid/crouton)

- list options: (`-r` = distros; `-t` = desktops)

  ```shell
  sudo sh ~/Downloads/crouton -r list
  sudo sh ~/Downloads/crouton -t list
  ```

- Install crouton (`-e` to encrypt)

  ```shell
  sudo sh ~/Downloads/crouton -e -r xenial -t gnome,xorg,xiwi
  ```

- `xorg` is for opening the linux desktop natively. `xiwi`
  is to be able to [run linux within a chrome
  window](https://github.com/dnschneid/crouton/wiki/crouton-in-a-Chromium-OS-window-(xiwi)).
  Whichever you put first will be the default; then use `sudo
  startgnome -X xiwi` to launch the in-a-window version.

  You can leave
  them both off (just `-t gnome`) and then you just get the native version.
  Or install with `xiwi` and then update to add `xorg` afterwards,
  using `sudo sh ~/Downloads/crouton -u -t xorg`. But then the second
  thing you add ends up as the default.

  And note that for the within-a-window version, you need the [crouton integration chrome extension](https://chrome.google.com/webstore/detail/crouton-integration/gcpneefbbnfalgjniomfjknbcgkbijom)

- Use `sudo startgnome` to start the desktop

- Note that the "search" key acts as a super key

- In settings:

  - mouse & trackpad: select "natural scrolling"
  - background: change to plain colors
  - sounds: in sound effects tab, turn off alert volume
  - date/time: set time to am/pm rather than 24 hr

- ctrl-alt-shift-forward (arrow key in top row) to switch from linux
  to chrome; ctrl-alt-shift-backward to go back to linux (the latter
  can have a *big* delay)

### Install stuff

- set locale

  ```shell
  sudo locale-gen "en_US.UTF-8"
  sudo dpkg-reconfigure locales
  ```

- `sudo apt install emacs mg gnome-terminal`

  (Seemed necessary to log out and log in again, to get `gnome-terminal`
  to work. At first, when running it, the window just didn't open.)

- Follow [Jenny's
  instructions](https://github.com/jennybc/operation-chromebook) to
  install R and RStudio. (I skipped the bit about the old version of
  gstreamer; latest version seemed to work fine.)

- Also follow [Jenny's
  instructions](https://github.com/jennybc/operation-chromebook) to
  install Minecraft. One clarification: Having made `Minecraft.jar`
  executable, you can launch it from a file browser by
  double-clicking, but not from the command line. To launch from the
  command line, make an executable bash script with the full path to
  `Minecraft.jar`:

  ```shell
  #!/bin/bash

  java -jar /home/kbroman/games/minecraft/Minecraft.jar
  ```

- I installed Firefox with `sudo apt install firefox`.
  To use gnome extensions, also need [Gnome shell
  integration](https://addons.mozilla.org/en-US/firefox/addon/gnome-shell-integration/)
  add-on. Also need to install the "native host connector" with `sudo apt install chrome-gnome-shell`

- Could also install chrome:

  - Download from <https://www.google.com/chrome/browser/desktop/index.html>
  - Install with `sudo dpkg -i google-chrome-*.deb`
  - Needed libappindicator1; used `sudo apt --fix-broken install`
  - Go to <https://extensions.gnome.org>
  - Install the [gnome shell integration
    extension](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep?hl=en)
  - Install the "native host connector" with `sudo apt install chrome-gnome-shell`
  - All this to install a [log-out button extension](https://extensions.gnome.org/extension/1143/logout-button)
  - Chrome (annoyingly) asks for a keyring password. There are [ways
    to disable
    that](https://askubuntu.com/questions/31786/chrome-asks-for-password-to-unlock-keyring-on-startup)


### Extra stuff

- To have a terminal open automatically, press <super> and search for
  "startup", to open "Startup Applications". Add `gnome-terminal`.

- For connecting to [eduroam](https://www.eduroam.us/), see
  <https://kb.wisc.edu/page.php?id=22075>

- For connecting to Wisc VPN, see
  <https://kb.wisc.edu/helpdesk/page.php?id=54507>




### Connecting to locally networked computers

I wanted to be able to connect to a computer on my local network,
`bromine.local`, that's running a minecraft server. But I wasn't
finding it by name, and `ping bromine.local` didn't work either
("host name not found").

But I found the IP address by pinging the name on my mac laptop. Using
that, I could both ping and connect to the minecraft server using the
IP.

But the following worked to determine the IP address:

```shell
avahi-resolve -n bromine.local
```

Actually, I had to run it twice. The first time it gave what looked
like sort of like hex values, but _much_ bigger numbers than they
should be. But then the second and subsequent times it worked.

On the linux side, I needed to fire up a daemon first. (On the
chromium side, seems like the daemon is already running.)

```shell
sudo avahi-daemon
```

I installed both tools using `sudo apt install avahi-utils` (which
also installed `avahi-daemon`).

And note that once the `avahi-daemon` was running, I could use
`bromine.local` in both ping and in minecraft.


### Other issues

- When running `sudo apt update` I'm often getting an error like

  ```
  E: Method http as died unexpectedly!
  E: Sub-process http received a segmentation fault.
  ```

  Not sure what to do. Tried logging out of linux and re-installing
  with crouton

  ```
  sudo sh ~/Downloads/crouton -n xenial -u -u
  ```
