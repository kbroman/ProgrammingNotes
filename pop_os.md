## Pop!_OS

Notes regarding [System76](https://system76.com)'s
[Pop!_OS](https://system76.com/pop) flavor of Ubuntu.
(See [the documentation](pop.system76.com/docs).)

- To move an app from one desktop to another:
  - go to the desktop with the app of interest
  - click Super
  - drag the app to the miniturized desktops on the right
  - alternatively, super-shift-up/down

- To move an app between monitors, use super-shift-left/right

- Alt-space to open a window's menu; includes an option to move the
  window to desktop above or below

- Copy/paste within terminal: Need to use ctrl-shift-c/v

- Copy/paste other places: Use just ctrl-c/v

- Super-A open applications

- Super-L lock screen

- Super-W close window

- Super-T open a terminal

- Super-D show desktop (doesn't seem to work)

- Super-P cycle display modes (doesn't seem to work)

- In terminal, ctrl-shift-left click on an URL to open in browser





### Upgrading to Pop!_OS 24.04

- change settings for desktop
  - appearance: accent color, square style, active window hint size 1,
    gaps around tiled windows 1
  - dock: left side, auto-hide, smaller size

- display settings: scale 125%

- input devices settings: "natural scrolling" for both mouse and touchpad

- re-install apps

  x R
  X Simplenote
  X RStudio
  X 1Password
  X Globalprotect VPN
  X Moneydance
  X duplicati
  X Tunnelbear

- start-up apps: removed deja-dup

- Network connection

  - needed to add "normal" wired connection profile
    (because it saved just my "direct connection" profile with static
    IP 10.0.0.1 that I use to directly connect two laptops)

- install R

  ```shell
  sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
  sudo apt install --no-install-recommends r-base
  ```

- install simplenote from [here](https://github.com/Automattic/simplenote-electron/releases/tag/v2.24.0)

  - `Simplenote-linux-2.24.0-amd64.deb`

- install 1password from [here](https://1password.com/downloads/linux)

- install rstudio from [here](https://posit.co/download/rstudio-desktop/)

  - Needed `sudo apt install --fix-broken`

- install GlobalProtect from file I'd saved

- install moneydance from file I'd saved
  (or from [here](https://infinitekind.com/download-moneydance-personal-finance-software))

- install duplicati from [here](https://duplicati.com/download)

- create a bootable thumb drive for Pop!_OS 24.04

  - see <https://support.system76.com/articles/live-disk/>

- Tunnelbear VPN settings were still there, but seem to need to enter
  password every time

- install cosmic applets

  - minimon
  - tempest (for weather)
  - dictionary
  - clipboard-manager

- needed to set up yubikey in cosmic

  In the file `/etc/pam.d/cosmic-greeter`,
  add `auth [tab] required [tab] pam_u2f.so`
  just after the line with `@include common-auth`

- Settings: desktop -> panel

  - remove "Activities" and "Workspaces" buttons
  - move date/time to far left
  - move minimon to center
  - make the panel a little bigger

- Settings: desktop -> workspaces

  - check "workspaces span displays" under multi-monitor behavior

- Settings: keyboard -> custom shortcuts

  - remove super-t as shortcut for (cosmic) terminal

  - custom shortcut: super-t for gnome-terminal

  - custom shortcut: super-c for gnome-calculator

- Eduroam: just needed to add login and password

- Install "smile" emoji picker

- Set up r2u using instructions [here](https://github.com/eddelbuettel/r2u?tab=readme-ov-file)

- Install espanso (for Wayland) using instructions [here](https://espanso.org/docs/install/linux/#deb-wayland)

  - matches in `~/.config/espanso/match/base.yml`

- Install npm and coffeescript

  - `sudo apt install npm`
  - `sudo npm install -g coffeescript`
  - `sudo npm install -g yarn`

  Also [`gistup`](https://github.com/mbostock/gistup):

  - `sudo npm install -g gistup`

  Also some others

  - `sudo npm install -g babel-core uglify-js uglifycss`


---


### Problems

- emacs problems

  - getting warnings from polymode
    (removed polymode from `~/.emacs.d/elpa/`)

- cosmic terminal problems

  - keyboard shortcuts for switching between tabs messes with those
    for emacs (specifically ctrl-shift-2)

  - also ctrl-shift-_ for undo isn't working

  - changed ctrl-shift-[0-9] to alt-[0-9] but still couldn't use my
    emacs bindings

  - switching back to gnome-terminal, which is still available and works
