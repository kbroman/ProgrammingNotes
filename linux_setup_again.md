## Linux setup

I got a new linux laptop, an
[Oryx Pro](https://system76.com/laptops/oryx) from
[System76](https://system76.com). This document describes what I did
when setting it up.

(I later purchased a System76 [Galago
Pro](https://system76.com/laptops/galago); I made some changes to the
instructions below, the second time around.)

(I later purchased a System76 [Darter
Pro](https://tech-docs.system76.com/models/darp8/README.html); I made further changes.)

(I later purchased a newer System76 [Darter Pro](https://tech-docs.system76.com/models/darp11/README.html).)

I had them install their [Pop!_OS](https://system76.com/pop) which is basically Ubuntu but
with some re-configured sessions and different choices of included
apps.

1. Log in for the first time, creating a new account

   - Set up including ability to connect google account.
   - That also had an option for Microsoft Exchange, so I briefly
     tried to connect to the UW-Madison Office 365, but it didn't work
     immediately so I moved on.

2. Connect to the internet (wired)

   - Plugged in a cable and it just worked.

3. Opened firefox and logged in

4. Software update

   ```
   sudo apt update
   sudo apt list --upgradable
   sudo apt upgrade
   ```

5. Install emacs and mg

   ```
   sudo apt install emacs mg
   ```

*6. Connect to the internet (wifi), using eduroam

   - See <https://kb.wisc.edu/helpdesk/page.php?id=25020>
   - Eduroam Configuration Assistance Tool, which gives a python
     script to download

7. Get UW-Madison VPN working

   Now using GlobalProtect, instructions at
   <https://kb.wisc.edu/helpdesk/page.php?id=105971>

   - Download and extract `PanGPLinux-[version].tgz` from
     <https://www.net.wisc.edu/vpn/clients/>
   - This gives a `GlobalProtext_UI_deb-[version].deb` file, to install via
     `sudo dpkg -i GlobalProtect_UI_deb-*.deb`.
   - Use `globalprotect launch-ui`
   - Use NetID and password; use `[username]_1` for static IP.
   - type `1` to have it push a DUO verification to your phone
   - the download page wasn't working, so copied over from other
     computer; it asked for VPN address, which is `uwmadison.vpn.wisc.edu`
     (now using `smph.vpn.wisc.edu`)

8. ssh keys + connect to github

   - [created new ssh
     key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   - used `ssh-keygen -t ed25519`
   - installed xclip with `sudo apt install xclip`
   - pasted to clipboard with `xclip -sel clip < ~/.ssh/id_rsa.pub`
   - At github, settings -> ssh and gpg keys -> New SSH key
   - Tested it out by cloning `git clone git@github.com:kbroman/ProgrammingNotes`
   - Also add the key to [bitbucket](https://bitbucket.org)
   - Trying to commit change to the repository, was reminded to set up git:

     ```
     git config --global user.email "kbroman@gmail.com"
     git config --global user.name "Karl Broman"
     git config --global core.editor "mg"
     git config --global core.excludesfile "/home/kbroman/.gitignore_global"
     ```

9. Install R

  - Install a bunch of linux stuff

    ```shell
    sudo apt install xauth xorg libx11-dev openbox
    sudo apt install libglu1-mesa-dev libfreetype6-dev
    sudo apt install libtiff-dev libfftw3-dev
    sudo apt install gfortran-9 libgdal-dev libproj-dev
    sudo apt install libcurl4-openssl-dev libssl-dev
    sudo apt install libxml2-dev libssh2-1-dev
    ```

  - Set up secure apt

    ```shell
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    ```

  - Add the following line to `/etc/apt/sources.list`

    ```
    deb https://cloud.r-project.org/bin/linux/ubuntu/ jammy-cran40/
    ```

  - Install R

    ```
    sudo apt update
    sudo apt install software-properties-common
    sudo apt update
    sudo apt install r-base r-recommended
    ```

  - Copy over `.Rprofile` and `.Renviron`; both needed a bit of editing

  - Need `r-cran-sqlite`?

  - For checking configure scripts in packages, needed `sudo apt install devscripts`
    (would get a warning otherwise)
  - Install some packages: tidyverse, broman, qtl, qtlcharts, qtl2, devtools
  - For the [imager package](https://cran.rstudio.com/package=imager),
    I got an error about X11. I ended up installing a bunch more
    ubuntu things. Some of these may not be necessary; was looking at
    what was needed for the [rgl package](https://cran.rstudio.com/package=rgl).

  - In some cases, `R CMD check` needs `checkbashisms`, which is
    installed with `devscripts`:

    ```
    sudo apt install devscripts
    ```


10. Install ess and other emacs modes (mostly cloned from GitHub; all
    placed in `~/.emacs.d`) and edit `~/.emacs` file.

    - [ess](https://ess.r-project.org)
    - [magit](https://github.com/magit/magit) (and
      dependencies [dash](https://github.com/magnars/dash.el),
      [with-editor](https://github.com/magit/with-editor),
      [magit-popup](https://github.com/magit/magit-popup),
      [ghub](https://github.com/magit/ghub),
      [git-modes](https://github.com/magit/git-modes))
    - [dracula-theme](https://github.com/dracula/emacs)
    - [my own fork of polymode](https://github.com/kbroman/polymode)
    - [arduino-mode](https://github.com/bookest/arduino-mode)
    - [markdown-mode](https://github.com/jrblevin/markdown-mode)
    - [d-mode](https://github.com/Emacs-D-Mode-Maintainers/Emacs-D-Mode)
    - [adoc-mode](https://github.com/sensorflo/adoc-mode) (for
      asciidoc)
    - [coffee-mode](https://github.com/defunkt/coffee-mode)
    - [inf-ruby](https://github.com/nonsequitur/inf-ruby)
    - [emacs-pry](https://github.com/jacott/emacs-pry) (another
      interactive ruby)

    I also wanted
    [html-helper-mode](http://download.savannah.gnu.org/releases/baol-hth/),
    but I've not gotten it working yet.

11. Install LaTeX (texlive)

    - I just did plain `sudo apt install texlive-full`

12. Install DropBox via Pop_Shop, but there are two choices and you
    want the one that says "Sync your files..." rather than "Access
    your files..."

13. Install SimpleNote (Pop_Shop has old version so get amd64 deb file
    from [github](https://github.com/Automattic/simplenote-electron/releases/))

14. Install Zoom via Pop_Shop

15. Changed hostname by editing the files `/etc/hostname` and `/etc/hosts`

    - replace `popos` or whatever with what you want, single line in
      `/etc/hostname` and on the line with `128.0.1.1` in `/etc/hosts`

16. Connect to printer

    - When I got home and connected to my home wifi, it automatically
      detected and added our printer. And it just worked: opened a PDF
      in evince and was able to print a couple of pages double-sided
      and in color.

17. Install Google Chrome

    - Download from <https://www.google.com/chrome/browser/desktop/index.html>
    - Install with `sudo dpkg -i google-chrome-*.deb`
    - Needed libappindicator1
    - Used `sudo apt --fix-broken install`

*18. Connect a USB stick

    - Plug into USB port and it shows up in `/media/kbroman`
    - Before removing, use `umount /media/kbroman/[drive name]`
    - Create a shortcut

      ```
      ln -s /media/kbroman/BROMAN ~/Key
      ```

19. Install RStudio

    - Download Ubuntu 22 `.deb` file from
      <https://www.rstudio.com/products/rstudio/download>
    - `sudo dpkg -i rstudio*.deb`
    - error re `libjpeg62`
    - `sudo apt install libjpeg62`
    - Needed to zoom in to the greatest extent or all of the dialogs were tiny
    - Needed to change CRAN mirror (in Tools -> global options ->
      packages) away from rstudio to something with https to avoid the
      warning at startup


20. Link to pandoc and quarto that shipped with RStudio
    (see <https://github.com/rstudio/rmarkdown/blob/main/PANDOC.md>)

    ```
    sudo ln -s /usr/lib/rstudio/resources/app/bin/quarto/bin/tools/x86_64/pandoc /usr/local/bin/
    sudo ln -s /usr/lib/rstudio/resources/app/bin/quarto/bin/quarto /usr/local/bin/
    ```


21. Okular pdf reader

    - `sudo apt install okular`
    - Installs a _ton_ of dependencies
    - Make it the default app for PDFs:
      - Open folder and right click on a PDF
      - Select Properties and then the "Open With" tab
      - Choose okular and click "Set default"
    - Was getting a bunch of warnings. Got some of them to go away with:

      ```
      sudo apt install breeze-icon-theme elementary-icon-theme
      ```

      But some remaining warnings:

      ```
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/16/"
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/22/"
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/24/"
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/32/"
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/48/"
      Invalid Type= "Scaleable" line for icon theme:  "/usr/share/icons/pop-os-branding/round-logos/64/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/16/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/22/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/24/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/32/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/48/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/64/"
      Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/128/"
      Icon theme "Mint-X" not found.
      ```

    - Tried also `sudo apt install oxygen-icon-theme`

    - Tried installing [mint themes](https://www.gnome-look.org/p/1175954/)


22. Additional packages

    ```
    sudo apt install gnome-tweaks
    ```


23. Create a `start` script that acts like `open` on a Mac, as a
    little shell script that just calls `xdg-open` repeatedly for
    each command-line argument. Placed this in `~/.local/bin`

    ```
    #!/bin/bash
    # loop over command-line arguments and open each with xdg-open

    for file in "$@"
    do
        xdg-open "$file" >& /dev/null  # ">& /dev/null" to suppress all warnings
    done
    ```


24. Get terminal to open at startup

    - Super key and type "Startup"
    - Click "Add"; for the command, use "`gnome-terminal`"
    - To start at a particular size and position, use like

      ```
      gnome-terminal --geometry=960x990+0+0
      ```

25. Testing webcam

    - Look at <https://help.ubuntu.com/community/Webcam>

    - Install cheese (it's like "photobooth" on Mac)

      ```
      sudo apt install cheese
      cheese
      ```

26. Download
    [moneydance](https://infinitekind.com/download-moneydance-personal-finance-software)

    - Available for linux as well as Mac :)
    - Downloaded `.deb` file; right click and "open" in chrome when it
      was done downloading, and it opened
      [Eddy](https://github.com/donadigo/eddy), a debian package
      installer.

27. Color picker, [gpick](http://www.gpick.org/)

    ```
    sudo apt install gpick
    ```

28. Copy stuff into `.bashrc`

29. Install some more packages with `sudo apt install`

    - `enscript` (for making PS files from text files, rotated or 2 column)
    - `gv` (ghostview, for viewing PS files)
    - `ubuntu-restricted-extras` (allows reading DVDs etc)

30. Install Inconsolata font

    ```
    sudo apt install fonts-inconsolata
    sudo fc-cache -fv
    ```

31. Install a bunch more programs

    - `vlc` (video player)
    - `calibre` (organizes ebooks)

32. Install espanso (much better than autokey); customizations in `~/.config/espanso/match/base.yml`

    ```shell
    sudo apt install libnotify-bin
    sudo apt install snapd
    sudo snap install espanso --classic
    espanso start
    ```

    copy over stuff from `~/.config/espanso`


33. Install npm and coffeescript

    - `sudo apt install npm`
    - `sudo npm install -g coffeescript`
    - `sudo npm install -g yarn`

    Also [`gistup`](https://github.com/mbostock/gistup):

    - `sudo npm install -g gistup`

    Also some others

    - `sudo npm install -g babel-core uglify-js uglifycss`

34. Install ruby (not sure whether I really need this)

    - `sudo apt install ruby-dev` (gives version 3.0.2p107; close enough?)

35. Install java

    ```
    sudo apt update
    sudo apt install default-jre default-jdk
    ```

    Test that it's working:

    ```
    java -version
    javac -version
    ```

36. Install Minecraft; see <https://minecraft.net/en-us/download/>

    - Download `Minecraft.deb` and install with `sudo dpkg -i Minecraft.deb`.


37. Install 1Password (needed `gnupg2`); download from
    <https://1password.com/downloads/linux/>

    ```
    sudo dpkg -i 1password-latest
    sudo apt install --fix-broken
    ```

38. More stuff via `sudo apt install`

    - `pdftk` (pdf tools) [now it suggests `pdftk-java` instead)
    - tried installing `pdfnup` but it seems it's included with
      texlive; actually no longer included in texlive. got it from
      <https://github.com/rrthomas/pdfjam-extras>
    - `handbrake` (for ripping DVDs)
    - `clementine` (music app)
    - `libnotify-bin` (enables you to create desktop notifications
      with `notify-send`; so in R you could do like
      `system('notify-send "R is done!"')`)
    - `trash-cli` (move files to "trash" via the command line (`trash`
      in place of `rm`)

    Stuff I left for future:

    - `rclone` (like rsync for cloud storage)
    - `filezilla` (ftp client)
    - `pinta` (like MS paint)
    - `gimp` (like photoshop)
    - `inkscape` (like illustrator)
    - `k3b` (for burning CDs)


39. [Gnome extensions](https://extensions.gnome.org)

    - (Can install, uninstall, and configure extensions within browser)
    - [Clipboard indicator](https://extensions.gnome.org/extension/779/clipboard-indicator)
      (gives clipboard history)
    - [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
    - [emoji selector](https://extensions.gnome.org/extension/1162/emoji-selector/)
      (also did `sudo apt install fonts-emojione`)
    - [gtile](https://extensions.gnome.org/extension/28/gtile/) (tile
      windows with a grid)
        - select window you want to resize
        - use Super-Enter (on number key pad) to open gtile
        - click one corner position and then the other on the grid
        - esc to exit
        - also use Super-Alt-[keypad numbers]
        - In Pop_OS! 20.04, disabled the pop shell extension
          (with Tile Windows), disabled in the extensions app
    - [Refresh wifi connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
      (adds a refresh button to the wifi connection dialog)
    - [AppIndicator](https://extensions.gnome.org/extension/615/appindicator-support/)
      used by dropbox, and seems to help ensure that all apps
      (including globalprotect) are shown in the menubar)
    - [Audio Output Switcher](https://extensions.gnome.org/extension/751/audio-output-switcher)/
    - [system-monitor](https://extensions.gnome.org/extension/3010/system-monitor-next/)
      (also needed `sudo apt install gir1.2-gtop-2.0`, and to log out
      and back in again)

40. Install [Slack](https://slack.com/downloads/linux) from Pop_Shop

41. Set up backups

    - Install Deja Dup via "Pop Shop"

    - Used command-line program `gnome-disks` to change to name of my
      extra hard drive. (Select the drive, click the gears, choose
      "Edit Filesystem...")

    - Set up Deja Dup for a daily backup of my home folder, ignoring
      the Downloads folder.

    - Ignore the folders `~/Dropbox` and `~/VirtualBox VMs` and `~/ISOs`

    - selected to backup to local folder, and to the backup drive and
      a folder I created there

    - need to edit `/etc/fstab` to get the disk to auto-mount
      - Use "Disks" app to find partition address like
        `/dev/nvme1n1p1`
      - edit `/etc/fstab` with a line like

        ```
        /dev/nvme1n1p1  /media/kbroman/Broster3Backup  auto  nosuid,nodev,nofail,x-gvfs-show  0  0
        ```

---

    - also setup backup with duplicati using two external drives
      ([transfer settings to the new machine](https://docs.duplicati.com/detailed-descriptions/migrating-duplicati-to-a-new-machine))

42. Copy over music

    - Used `rsync`; issue of having spaces in paths, but can do like
      this (note the backslashes _and_ quotes):

      ```
      rsync -a "fig.local:Music/iTunes/iTunes\ Music/They\ Might\ Be\ Giants" .
      ```


44. Was looking at finding a better linux terminal, but I think the
    standard gnome terminal will be fine for me.

    - Can open a new terminal in an additional tab with
      ctrl-shift-T
    - Switch between tabs with ctrl-PgUp and ctrl-PgDn
    - Alt-1, Alt-2, etc., to switch to a particular tab (by number, up
      to 9; Alt-0 for tab 10)
    - See all keyboard shortcuts by going to Edit -> Preferences ->
      Shortcuts

45. Install [gitg](https://wiki.gnome.org/Apps/Gitg/), a git GUI similar to
    [gitx](https://gitx.frim.nl/) (which is Mac only)

    ```
    sudo apt install gitg
    ```

46. [Tunnelbear VPN](https://www.tunnelbear.com/blog/setting-up-tunnelbear-on-linux/)

    - `sudo apt install network-manager-openvpn-gnome`

    - `mkdir ~/.tunnelbear_config`

    - Grab [config
      files](https://tunnelbear.s3.amazonaws.com/support/linux/openvpn.zip)
      and unzip to the above `.tunnelbear_config` directory

    - Open Network settings; click plus sign by VPN and choose "Import
      from file"; find directory created above and select the file for
      the desired country. Add email address and tunnelbear password.
      Click "Add".

    - To start/stop: turn on/off VPN in network settings via status
      bar in top-right of display

    - To test:
        - [check your IP](https://bearsmyip.com/)
        - check for DNS leaks with "Extended test" at [dnsleaktest.com](https://www.dnsleaktest.com/)

    - **The above didn't work**, but was able to create by hand

      - getting errors when trying to load from file, or from command
        line
      - by hand, e.g. TunnelBear Canada: select
        OpenVPN, give Gateway as `ca.lazerpenguin.com:443` and
        Authentication `Password` with email and tunnelbear password,
        and then `CACertificate.crt` from `~/.tunnelbear_config/openvpn`

50. [kmag](https://stackoverflow.com/a/26418432) useful for simulating
    color blindness: `sudo apt install kmag`


51. Regarding battery life, see [this system76
    article](https://support.system76.com/articles/battery/) which
    recommends:

    ```
    sudo apt install tlp tlp-rdw --no-install-recommends
    sudo tlp-stat

    sudo apt install powertop
    sudo powertop -c
    sudo powertop --help=report
    sudo powertop --auto-tune
    ```

    Configure `tlp` by editing `/etc/default/tlp`.

52. Made a keyboard shortcut to open toodledo.com in a web browser:

    - open Settings -> Keyboard
    - Scroll to the bottom of the Keyboard Shortcuts and click the +
    - Create a new shortcut (I used ctrl-alt-T) with the command
      `firefox https://toodledo.com/tasks/index.php`

    - Additional shortcuts:

      - flameshot
      - navigation: move window one monitor to left/right, move window
        one workspace up/down, using shift+super+arrow


53. I installed Anaconda by downloading the `.sh` script from
    [its web
    site](https://www.anaconda.com/distribution/#download-section)
    and running `bash Anaconda-*.sh`. I chose to install it in
    `~/.anaconda3` and had it modify my `.bashrc` file.

54. Installed Julia with `sudo apt install julia` but this gave
    version 1.0.1 which seems really old (current is 1.1 and long-term
    support release is 1.0.3). So I instead

    - downloaded the `.tar.gz` file with "generic linux
    binaries", from <https://julialang.org/downloads/>

    - extracted into `/usr/local/src`

    - created symbolic link to `/usr/local/src/julia-1.1.0/bin/julia`
      in `/usr/local/bin`

    - ran `julia` and installed IJulia to enable use in jupyter
      notebooks

      ```
      using Pkg
      Pkg.add("IJulia")
      ```

      then when running `jupyter notebook`, can click "New" and the
      options are both "Python3" and "Julia1.1.1"

55. Mouse acceleration (also want touchpad acceleration, but there
    doesn't seem to be a setting for it):

    ```
    gsettings list-keys org.gnome.desktop.peripherals.mouse
    gsettings list-keys org.gnome.desktop.peripherals.touchpad
    sudo gsettings get org.gnome.desktop.peripherals.mouse accel-profile
    sudo gsettings set org.gnome.desktop.peripherals.mouse accel-profile 'adaptive'
    ```

    Can also change these settings with the gnome tweaks gui.

56. Installed the mini-emacs application, `mg` via

    ```
    sudo apt install mg
    ```

    Made it the default for git commit messages by editing
    `~/.gitconfig`. More than sufficient for that, and way faster to
    start up.

57. Setup playback of dvds

    ```
    sudo apt install libdvd-pkg
    sudo dpkg-reconfigure libdvd-pkg
    ```

58. Oryx Pro fan can be really loud. To lower it, use
    [clevo-indicator](https://github.com/davidrohr/clevo-indicator)

    ```
    sudo apt install libappindicator3-dev
    git clone https://github.com/davidrohr/clevo-indicator
    cd clevo-indicator
    make
    ```

    To use: put `bin/clevo-indicator` in `~/.local/bin/`

    ```
    sudo clevo-indicator
    sudo clevo-indicator set 50
    sudo clevo-indicator setg 50
    ```

59. [neofetch](https://github.com/dylanaraps/neofetch) provides system info at the command-line

--

- Install ccache and use for compiling R

  - `sudo apt install ccache`
  - In `~/.R`:

- Additional possible gnome extensions:
  - [Places status indicator](https://extensions.gnome.org/extension/8/places-status-indicator/)
  - [Pomodoro timer](https://gnomepomodoro.org/)



---

### Stuff that didn't work:


1. Set up Apple magic mouse via bluetooth settings

   - It came up with a weird name; I had to go back to Mac and pair it
     and then rename it and then back to pair again with the linux
     laptop
   - Scrolling speed was deathly slow. Followed instructions
     at <https://askubuntu.com/a/262730>. In particular, I used:

     ```
     options hid_magicmouse scroll-speed=60 scroll-acceleration=2
     ```
   - **FIX ME**: want scrolling to go in the opposite direction
   - **FIX ME**: after restarting and messing with the trackpad (not
     sure what I did), the mouse stopped working.


2. Try to get Apple Magic Trackpad working

    - Looking at [Touchégg](https://github.com/JoseExposito/touchegg/wiki/How-to-compile-Touch%C3%A9gg-source-code)

      ```
      git clone git://github.com/JoseExposito/touchegg.git
      sudo apt-get build-dep touchegg
      qmake
      make
      sudo make install
      ```

    - **FIX ME**: At present, it's not working
    - Removed Touchégg with `sudo make uninstall`

----

### Problems

1. I had some gnome extensions that
weren't working but that I couldn't delete. Followed [these
instructions](https://unix.stackexchange.com/a/403674):

  - Look in `~/.local/share/gnome-shell/extensions`
    and also `/usr/share/gnome-shell/extensions`
  - Delete the directories for extensions you want to get rid of
  - Reload gnome-shell by pressing ALT+F2, typing `r`, and pressing ENTER.
