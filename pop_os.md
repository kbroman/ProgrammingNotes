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

- To restart Cosmic (equivalent to restarting gnome-shell)

  ```bash
  killall -3 cosmic-panel
  ```



### Upgrading to Pop!_OS 24.04

- change settings for desktop
  - appearance: accent color, square style, active window hint size 1,
    gaps around tiled windows 1
  - dock: left side, auto-hide, smaller size

- click the tiling icon in the panel
  - select "Tile current workspace"
  - select "Tiled" for "New workspace behavior"

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

- Install "emote" emoji picker from cosmic store

- Settings: keyboard -> custom shortcuts

  - custom shortcut: super-c for gnome-calculator
    (command = `gnome-calculator`)

  - custom shortcut: super-e for emote (emoji picker)
    (command = `flatpak run com.tomjwatson.Emote`)

- Eduroam: just needed to add login and password

- In cosmic terminal, set default font to "Liberation Mono"

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


- Change pbcopy/pbpaste

  - I have pbcopy (pbpaste) as aliases for `xsel --clipboard --input`
    (and `--output`), but these don't work with Wayland.

  - change to `wl-copy` and `wl-paste` in the wl-clipboard package

---


### Problems

- emacs problems

  - getting warnings from polymode
    (removed polymode from `~/.emacs.d/elpa/`)

- cosmic terminal problems

  - keyboard shortcuts for switching between tabs messes with those
    for emacs (specifically ctrl-shift-2)

  - also ctrl-shift-_ for undo isn't working (but can use c-x u)

  - changed ctrl-shift-[0-9] to alt-[0-9] but still couldn't use my
    emacs bindings

  - switching back to gnome-terminal, which is still available and works

  - to change default terminal: set default terminal in
    cosmic settings -> applications -> default applications

  - also having trouble with set-mark (ctrl-shift-@)
    (but can use ctrl-space)

- Gnome-terminal problems

  - had switched to use gnome-terminal rather than cosmic-term because
    of the undo issue, and the issue of tabs

  - but I've been having problems with copy/paste from other
    applications to gnome-terminal, so switching back to cosmic-term

  - rather than using terminal tabs, I'm opening separate terminals
    and using window stacking (super-s to create a window stack)

- Frequent difficulty connect Dell monitors via thunderbolt

  - get message like "Thunderbolt output not available"

  - solution seems to be:

    - unplug monitor cable and reboot laptop

    - right after entering password to decrypt drive, plug in the
      thunderbolt cable

    - leave laptop lid open until i've logged in, then close laptop
      and readjust windows

- Cosmic-terminal problems

  - switching back to gnome-terminal, because the problems with
    cosmic-term were bigger: would lock up when pasting, or with a
    long-running job

  - just change default terminal in
    Cosmic settings -> Applications -> Default Applications -> Terminal

  - can't see how to have cosmic open a gnome-terminal at start-up.
    The start-up applications options seem only to select specific
    applications, and not to run any general bit of code at the shell.
    🙁

- moneydance problems

  - have problems when adding items, as any drop-down menu
    (and particularly the categories one) goes a bit crazy so you
    can't select anything and you're stuck until you can jump to a
    different field

  - also, occasionally having moneydance start up but then disappear.
    like it's running but without a window. I thought i'd figured out
    a solution to this but cancelling before entering password and
    then selecting database and then entering password, but lately
    that's not working either

  - finally, removing `~/.moneydance/config.dict` seemed to work.
    needed to re-enter my license, though
