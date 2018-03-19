## Linux issues


- Periodic troubles logging in, with a spinning circle and then a
  message "Authentication error" repeat some number of times.
  Sometimes it ends up logging in, sometimes repeats a ton of times so
  I eventually restart at which point all is fine.

  - System 76 suggested re-installing the login manager, gdm3

    ```shell
    sudo apt install --reinstall gdm3
    ```

  - Well, that didn't work, so following their second suggestion of
    purging and re-installing:

    ```shell
    sudo apt purge gdm3
    sudo apt install gdm3
    ```

    This didn't work, either.

  - [this page](https://ubuntuforums.org/showthread.php?t=2380381)
    suggests removing a bunch of stuff.

    ```shell
    sudo apt purge --auto-remove gdm3
    sudo apt purge --auto-remove gnome-shell
    sudo apt purge --auto-remove gnome-software
    sudo apt purge --auto-remove lightdm
    sudo apt purge --auto-remove gnome-session-bin
    sudo apt purge --auto-remove gnome-session-common
    sudo apt purge --auto-remove ubuntu-session
    sudo apt purge --auto-remove ubuntu-desktop
    ```

    In a couple of places, I was asked whether I want to use gdm3 or
    lightdm. I chose gmd3 in all cases.

    I then ran the following:

    ```shell
    sudo apt update
    sudo apt upgrade
    sudo apt install ubuntu-desktop
    ```

    I went ahead and tried installing all of the other stuff I'd
    removed, in reverse order of their removal, but it seems that when
    you install `ubuntu-desktop`, you install all of that stuff.

    This seems to have worked, but it means I'm now using the standard
    ubuntu desktop rather than the pop desktop.

    So I tried installing `pop-desktop`. It asked me to first
    install `sessioninstaller`, so I did:

    ```shell
    sudo apt install sessioninstaller
    sudo apt install pop-desktop
    ```

  - I ended up back at the same problem, so I tried removing
    `ubuntu-desktop` and then reinstalling it:

    ```shell
    sudo apt purge --auto-remove ubuntu-desktop
    sudo apt update
    sudo apt upgrade
    sudo apt install ubuntu-desktop
    sudo apt autoremove
    ```

    It did say "removing `pop-desktop` and `sessioninstaller`.

    Some amount of pop desktop styling still seems to be in place, and
    I'm having the same problem. So I'm going back to the more
    extensive purging followed by re-install of `ubuntu-desktop`.

  - It really seemed like `ubuntu-desktop` was going to solve the
    problem, but finally it resurfaced. The latest suggestion was to
    switch to `lightdm` (rather than `gdm3`).

    ```shell
    sudo apt install lightdm
    sudo dpkg-configure lightdm
    ```

    Makes a sound at startup, which I don't like. A [fix for
    that](https://bugs.launchpad.net/ubuntu/+source/unity-greeter/+bug/949782/comments/6):

    - create file `/usr/share/glib-2.0/schemas/50_unity-greeter`

    - Add the following lines:

      ```
      [com.canonical.unity-greeter]
      play-ready-sound = false
      ```

    - Run `glib-compile-schemas /usr/share/glib-2.0/schemas/` (but I
      get warning messages unless I use `sudo` with that)

- Sometimes when restarting from having been suspended, the wifi
  connects but there's no actual internet connection.

  I tried the following, suggested
  [here](https://www.howopensource.com/2014/12/ubuntu-restart-network/),
  but no luck.

  ```shell
  sudo service network-manager restart
  ```

  Re-starting does the trick.


- Having trouble with displays. In particular, getting the right
  setting on my external display, and having it work on its own,
  with the laptop's display off. Even better would be to use it with
  the laptop closed.

  The thing that seems to work: log in, select display settings (to
  have external display as single monitor), then close laptop (to
  suspend), then open laptop again

- Emoji fonts don't seem to work. For example, using them with
  autokey. Can paste them normally (though black-and-white) but they
  don't show up within autokey

- warnings etc from okular

  ```
  Icon theme "breeze" not found.
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/16/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/22/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/24/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/32/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/48/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/64/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/128/"
  Icon theme "Mint-X" not found.
  Icon theme "elementary" not found.
  Illegal icon group:  7
  ```

- Apple bluetooth magic mouse and magic trackpad


## Solved

- VPN not working with eduroam, though it does work with wired
  ethernet connection. Actually, a week later it seemed to work. Not
  sure why.
