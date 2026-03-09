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
  - RStudio
  - Moneydance
  Globalprotect VPN
  Tunnelbear
  1Password
  duplicati

- start-up apps:

  - remove gnome terminal and use cosmic terminal
  - duplicati, simplenote, ping

- Network connection

  - needed to re-add "normal" wired connection profile
    (because it saved just my "direct connection" profile with static
    IP 10.0.0.1 that I use to directly connect two laptops)

- re-install R

  ```shell
  sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
  sudo apt install --no-install-recommends r-base
  ```

- re-install simplenote from [here](https://github.com/Automattic/simplenote-electron/releases/tag/v2.24.0)

  - `Simplenote-linux-2.24.0-amd64.deb`

- install cosmic applets

  - minimon
  - weather
  - numbered workspaces
  - clipboard-manager

---

- emacs problems

  - getting warnings from polymode

- cosmic terminal problems

  - keyboard shortcuts for switching between tabs messes with those
    for emacs (specifically ctrl-shift-2)
