## Linux setup

I got a new linux laptop, an
[Oryx Pro](https://system76.com/laptops/oryx) from
[System76](https://system76.com). This document describes what I did
when setting it up.

(I later purchased a System76 [Galago
Pro](https://system76.com/laptops/galago); I made some changes to the
instructions below, the second time around.)

(I later purchased a System76 [Darter
Pro (darp8)](https://tech-docs.system76.com/models/darp8/README.html); I made further changes.)

(I later purchased a newer System76 [Darter Pro (darp11)](https://tech-docs.system76.com/models/darp11/README.html).)

I had them install their [Pop!_OS](https://system76.com/pop) which is basically Ubuntu but
with some re-configured sessions and different choices of included
apps.

1. Log in for the first time, creating a new account

   - Set up including ability to connect google account.
   - That also had an option for Microsoft Exchange, so I briefly
     tried to connect to the UW-Madison Office 365, but it didn't work
     immediately so I moved on.
   - Settings: Natural scrolling for mouse and trackpad; move dock to
     left side and hide it

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
     (now using `smph.vpn.wisc.edu`, but won't take `[username]_1`
     just `[username]`)

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
    - It hung up part-way through; got it to continue by pressing
      return multiple times

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

18. Connect a USB stick

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
    - Previously got a bunch of warnings, so used this:

      ```
      sudo apt install breeze-icon-theme elementary-icon-theme
      ```

    - Also tried `sudo apt install oxygen-icon-theme`

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

27. Color picker [gpick](http://www.gpick.org/), and image viewer [gthumb](https://gitlab.gnome.org/GNOME/gthumb)

    ```
    sudo apt install gpick gthumb
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
        - Disabled the "pop shell" extension
          (with Tile Windows); disabled it in the extensions app.
          Actually had to re-enable it, as when disabled, the super
          key stopped working
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
    Also Discord.

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

    - also setup backup with duplicati using two external drives
      ([transfer settings to the new
      machine](https://docs.duplicati.com/detailed-descriptions/migrating-duplicati-to-a-new-machine));
      copied over configuration from `~/.config/Duplicati/` (**2.5 GB**)

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

50. [kmag](https://stackoverflow.com/a/26418432) useful for simulating
    color blindness: `sudo apt install kmag`

    - It's a screen magnification tool; in menubar View → Color, you
      can choose different versions of colorblindness.

51. Regarding battery life, see [this system76
    article](https://support.system76.com/articles/battery/) which
    recommends:

    ```
    sudo apt install powertop
    sudo powertop -c
    sudo powertop --help=report
    sudo powertop --auto-tune
    sudo powertop --html=report.html
    ```

    - Previously there was discussion of `tlp` but now they say it's not
      compatible with `system76-power`.

    - The article also points to the tool `intel_gpu_top` for
      monitoring the integrated intel graphics. Install with

      ```
      sudo apt install intel-gpu-tools
      ```

    - Can check battery health with `upower -d`.

    - Control charging thresholds with `system76-power`.

      ```
      system76-power charge-thresholds 20 52
      ```

80. Made a keyboard shortcut to open toodledo.com in a web browser:

    - open Settings -> Keyboard
    - Scroll to the bottom of the Keyboard Shortcuts and click the +
    - Create a new shortcut (I used ctrl-alt-T) with the command
      `firefox https://toodledo.com/tasks/index.php`

    - Additional shortcuts:

      - navigation: move window one monitor to left/right, move window
        one workspace up/down, using shift+super+arrow

      - ctrl-alt-p for interactive screenshot. (screenshots saved to `~/Pictures/Screenshots`)

      - super-c for calculator

53. No longer installing Anaconda because they [changed their
    license](https://licenseware.io/retrospective-on-anacondas-2024-licensing-changes-what-they-mean-and-smarter-alternatives/).

    - Just going to use the built-in `python3`

54. Installed Julia with `sudo apt install julia` but it had a lot of
    problems. So installed followed the [official instructions]():

    ```
    curl -fsSL https://install.julialang.org | sh
    ```

    This put julia in `~/.juliaup/bin/julia`.

*55. Installed Jupyter

      ```
      sudo apt install jupyter
      ```

    - ran R and installed `IRkernel` package and then
      `IRkernel::installspec()`

      then when running `jupyter notebook`, can click "New" and the
      options are both "Python 3" and "R"

    - ran `julia` and installed IJulia to enable use in jupyter
      notebooks

      ```
      using Pkg
      Pkg.add("IJulia")
      ```

      then when running `jupyter notebook`, can click "New" and the
      options should include "Python 3", "R", and "Julia1.11.7"

56. Mouse acceleration (also want touchpad acceleration, but there
    doesn't seem to be a setting for it):

    ```
    gsettings list-keys org.gnome.desktop.peripherals.mouse
    gsettings list-keys org.gnome.desktop.peripherals.touchpad
    sudo gsettings get org.gnome.desktop.peripherals.mouse accel-profile
    sudo gsettings set org.gnome.desktop.peripherals.mouse accel-profile 'adaptive'
    ```

    Can also change these settings with the gnome tweaks gui.

57. Setup playback of dvds

    ```
    sudo apt install libdvd-pkg
    sudo dpkg-reconfigure libdvd-pkg
    ```

58. [neofetch](https://github.com/dylanaraps/neofetch) provides system info at the command-line

59. Install ccache and use for compiling R

    - `sudo apt install ccache`
    - In `~/.R/Makevars`:

      ```
      CC=ccache gcc
      CXX=ccache g++
      CFLAGS=-DNDEBUG -fpic -g -O2 -fstack-protector-strong -D_FORTIFY_SOURCE=2
      CXXFLAGS=-fpic -g -O2 -fstack-protector-strong -D_FORTIFY_SOURCE=2
      ```

60. Set up yubikeys as in [yubikeys.md](https://github.com/kbroman/ProgrammingNotes/blob/main/yubikey.md)

61. Install speedtest with `sudo apt install speedtest-cli`

62. Install some packages for Libre Office

    ```
     sudo apt-get install default-jre libreoffice-java-common
    ```
