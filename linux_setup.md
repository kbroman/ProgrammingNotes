## Linux setup

I got a new linux laptop, an
[Oryx Pro](https://system76.com/laptops/oryx) from
[System76](https://system76.com). This document describes what I did
when setting it up.

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

4. Connected to Office365

   - Settings → Online accounts
   - Microsoft Exchange → Add
   - email = (my biostat account)
   - custom: username = (my vanilla UW account, with @wisc.edu)
   - custom: server = outlook.office365.com
   - Use only for mail (deselect contacts and calendar)

5. Software update

   ```
   sudo apt update
   sudo apt list --upgradable
   sudo apt upgrade
   ```

6. Install emacs

   ```
   sudo apt install emacs25
   ```

7. Connect to the internet (wifi), using eduroam

   - Followed the instructions at <https://kb.wisc.edu/page.php?id=22075>

8. Get UW-Madison VPN working

   - Followed the instructions at <https://kb.wisc.edu/page.php?id=74947>
   - **FIX ME**: Didn't seem to work for me, though, in that I
     couldn't connect to BMI servers. I mean:
   - When running `sudo vpnc uwmadison.conf`, it did ask for my
     password and then (after a delay) said `VPNC started in
     background`, and when I did `ps aux | grep vpnc` I did see the
     process running, _but_ I couldn't ssh into the biostat servers
   - While vpnc is running, `ping broman-10.biostat.wisc.edu`
     indicates I'm not able to connect. Same when I use the IP address
     (that shows up when I ping without vpnc running). With vpnc
     running, I seem to lose my network connection completely.
   - Hmm...if I turn off wifi and connect with an ethernet cable, the
     vpn works and I can get to the biostat servers. So maybe it's an
     eduroam issue?
   - playing with turning wired and wifi on and off, I can no longer
     get a connection to anything at wisc.edu. Logging out and back in
     didn't help, but restarting the computer worked
   - works fine on my home wifi network, so maybe just an eduroam/vpnc issue


9. ssh keys + connect to github

   - [created new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   - installed xclip with `sudo apt install xclip`
   - pasted to clipboard with `xclip -sel clip < ~/.ssh/id_rsa.pub`
   - At github, settings -> ssh and gpg keys -> New SSH key
   - Tested it out by cloning `git clone git@github.com:kbroman/ProgrammingNotes`
   - Also add the key to [bitbucket](https://bitbucket.org)
   - Trying to commit change to the repository, was reminded to set up git:

     ```
     git config --global user.email "kbroman@gmail.com"
     git config --global user.name "Karl Broman"
     git config --global core.editor "emacs"
     git config --global core.excludesfile "/home/kbroman/.gitignore_global"
     ```

10. Copy over stuff from my desktop

    - Attached USB drive that I'd copied stuff to
    - Showed up in `/media/kbroman/[drive name]
    - Used `rsync -a` to copy stuff over
    - Got a bunch of errors like "`send_files failed ... Permission denied (13)`"
      - No errors if I use `sudo rsync`
      - But then `ls -l` shows that the owner and group are odd for the offensive files.
      - So followed with `sudo chown kbroman -R [blah]`
      - Also `sudo chgrp kbroman -R [blah]`
      - (seems like I'm doing it wrong, but so be it)
    - Afterwards, I used `sudo umount /media/kbroman/KarlBkStuff`
      (I think I maybe didn't need the "`sudo`".)

11. Set up mail in Geary

    - First tried setting up gmail; authentication didn't work
    - Needed to create an App-specific password; see
      <https://support.google.com/accounts/answer/185833>
    - Added the UW-Madison Office365 account too:
      - "Geary" in menu bar -> Accounts -> plus sign
      - Service -> Other
      - Settings as at <https://kb.wisc.edu/page.php?id=28427>
    - Also added my iCloud account, following instructions at
      <https://support.apple.com/en-in/HT202304>, including need to
      get an app-specific password at
      <https://appleid.apple.com/account/manage>
    - To control default font in messages, create a file
      `~/.config/geary/user-message.css`, for example with:

      ```
      body {
          font-family: Inconsolata;
          font-size: 150%
      }
      ```


12. Install R

   - See [instructions at digitalocean](https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-16-04-2)

     ```
     sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
     sudo add-apt-repository 'deb https://cran.rstudio.com/bin/linux/ubuntu artful/'
     sudo apt update
     sudo apt install r-base
     ```
  - Copy over `.Rprofile` and `.Renviron`; both needed a bit of editing
  - Also copy over `.rpushpullet.json`
  - Install some packages: tidyverse, broman, qtl, qtlcharts, qtl2, devtools
  - Needed `sudo apt install libcurl4-openssl-dev libssl-dev libxml2-dev libssh2-1-dev`
  - When installing qtl2, error when installing bit64 package
    ("Could not find function `bit_init()`")
  - Finally just did `sudo apt install r-cran-rsqlite`
  - After that, qtl2 installed fine


13. Install ess and other emacs modes (mostly cloned from GitHub; all
    placed in `~/.emacs.d`) and edit `~/.emacs` file.

    - [ess](https://ess.r-project.org)
    - [magit](https://github.com/magit/magit) (and
      dependencies [dash](http://github.com/magnars/dash.el),
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

14. Install LaTeX (texlive)

    - I just did plain `sudo apt install texlive-full`

15. Install DropBox

    - Download `.deb` file from <https://www.dropbox.com/install-linux>
    - Use `sudo dpkg -i dropbox_2015.10.28_amd64.deb`

16. Install SimpleNote

    - Following instructions at <https://www.dropbox.com/install-linux>
    - Download `.deb` file from <https://simplenote.com>
    - Need dependency: `sudo apt install pango1.0-0`
    - `sudo dpkg -i Simplenote-*.deb`

17. Install Skype

    - Download `.deb` file from <https://www.skype.com/en/get-skype/>
    - Need some dependencies: `sudo apt install gconf-service libgconf-2-4`
    - Install with `sudo dpkg -i skypeforlinux-64.deb`
    - Skype was starting automatically on restarting the computer; had
      to de-select an option in the settings
    - **FIX ME**: shows up _really_ small when screen is in high-def mode
    - Camera was not working initially, but when studying it, learned
      about `cheese` (like Mac photobooth; see more below) and it
      worked fine. So opened skype again and found the camera was
      working. Not sure what changed.


18. Changed hostname by editing the files `/etc/hostname` and `/etc/hosts`


19. Connect to printer

    - When I got home and connected to my home wifi, it automatically
      detected and added our printer. And it just worked: opened a PDF
      in evince and was able to print a couple of pages double-sided
      and in color.

20. Install Google Chrome

    - Download from <https://www.google.com/chrome/browser/desktop/index.html>
    - Install with `sudo dpkg -i google-chrome-*.deb`
    - Needed libappindicator1
    - Used `sudo apt --fix-broken install`


21. Connect a USB stick

    - Plug into USB port and it shows up in `/media/kbroman`
    - Before removing, use `umount /media/kbroman/[drive name]`


22. Install RStudio

    - Download Ubuntu 16.04+ `.deb` file from
      <https://www.rstudio.com/products/rstudio/download>
    - `sudo dpkg -i rstudio*.deb`
    - error re `libjpeg62`
    - `sudo apt install libjpeg62`
    - Needed to zoom in to the greatest extent or all of the dialogs were tiny
    - Needed to change CRAN mirror (in Tools -> global options ->
      packages) away from rstudio to something with https to avoid the
      warning at startup


23. Link to pandoc that shipped with RStudio
    (see <https://github.com/rstudio/rmarkdown/blob/master/PANDOC.md>)

    ```
    sudo ln -s /usr/lib/rstudio/bin/pandoc/pandoc /usr/local/bin
    sudo ln -s /usr/lib/rstudio/bin/pandoc/pandoc-citeproc /usr/local/bin
    ```


24. Okular pdf reader

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


25. Additional packages

    - `bin-libgnome2` (for `gnome-open` which acts like `open` on a Mac)
    - `gnome-tweak-tool`
    - `caffeine` (thought this didn't work initially, but there's no
      longer a little icon in the "panel"; rather it runs in the
      background and will turn off screen saver when there's an
      application in full screen mode)


26. Create a `start` script that acts like `open` on a Mac, as a
    little shell script that just calls `gnome-open` repeatedly for
    each command-line argument. Placed this in `~/.local/bin`

    ```
    #!/bin/bash

    for file in "$@"
    do
        gnome-open "$file"
    done
    ```


27. Get terminal to open at startup

    - Super key and type "Startup"
    - Click "Add"; for the command, use "`gnome-terminal`"
    - To start at a particular size and position, use like

      ```
      gnome-terminal --geometry 117x57+0+0
      ```

28. Testing webcam

    - Look at <https://help.ubuntu.com/community/Webcam>

    - Install cheese (it's like "photobooth" on Mac)

      ```
      sudo apt install cheese
      cheese
      ```

29. Download
    [moneydance](https://infinitekind.com/download-moneydance-personal-finance-software)

    - Available for linux as well as Mac :)
    - Downloaded `.deb` file; right click and "open" in chrome when it
      was done downloading, and it opened
      [Eddy](https://github.com/donadigo/eddy), a debian package
      installer.

30. Color picker, [gpick](http://www.gpick.org/)

    ```
    sudo install gipck
    ```

31. Copy stuff into `.bashrc`

32. Install some more packages with `sudo apt install`

    - `enscript` (for making PS files from text files, rotated or 2 column)
    - `gv` (ghostview, for viewing PS files)
    - `unbuntu-restricted-extras` (allows reading DVDs etc)
    -


33. Install Inconsolata font

    ```
    sudo apt install fonts-inconsolata
    sudo fc-cache -fv
    ```

34. Install a bunch more programms

    - `vlc` (video player)
    - `calibre` (organizes ebooks)
    - `autokey-gtk` (desktop automation)
    - `digikam` (organizing photos)

35. Install npm and coffeescript

    - `sudo apt install npm`
    - `sudo npm install --global coffeescript`

36. Install ruby (not sure whether I really need this)

    - `sudo apt install ruby-dev` (gives version 2.3.3; close enough?)

37. Install python-dev (not sure whether I really need this)

    - `sudo apt install python-dev python3-dev`

38. Install peek (screen recording)

    ```
    sudo add-apt-repository ppa:peek-developers/stable
    sudo apt update
    sudo apt install peek
    ```

39. Install java 8 (there's a java 9, but Minecraft still needs 8)

    Followed the instructions at <http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html>

    ```
    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java8-installer
    sudo apt install oracle-java8-set-default
    ```

    Test that it's working:

    ```
    java -version
    javac -version
    ```

40. Install Minecraft; see <https://minecraft.net/en-us/download/>

    - download `Minecraft.jar`
    - I placed in `/usr/local/lib` and then put a shell script in
      `/usr/local/bin/minecraft`

      ```
      #!/bin/bash
      # start minecraft
      gnome-open /usr/local/lib/Minecraft.jar
      ```


41. Install [keepassXC](https://keepassxc.org/download/)

    ```
    sudo add-apt-repository ppa:phoerious/keepassxc
    sudo apt update
    sudo apt install keepassxc
    ```

    (this took me a while because I kept typing `keypassxc` rather
    than `keepassxc`)

42. Mount exFAT drive connect to a router

    - Install `smbclient` and exFAT stuff

      ```
      sudo apt install smbclient exfat-fuse exfat-utils
      ```

    - List volumes

      ```
      smbclient -L //192.168.0.3
      ```

    - Mount the drive...was trying the following:

      ```
      sudo mount -t cifs -o username=kbroman //192.168.0.3/volume10/ /media/kbroman
      ```

      but got an error like one of these two:

      ```
      mount error(115): Operation now in progress
      mount error(112): Host is down
      ```

    - However, I was able to connect using the GUI file browser.
      Clicked "Other locations" and then typed `smb://192.168.0.3`

43. More stuff via `sudo apt install`

    - `pdftk` (pdf tools)
    - (tried installing `pdfnup` but it seems it's included with
      texlive)
    - `pinta` (like MS paint)
    - `handbrake` (for ripping DVDs)
    - `gimp` (like photoshop)
    - `inkscape` (like illustrator)
    - `shutter` (image capture)
    - `k3b` (for burning CDs)
    - `banshee` (music app)
    - `rclone` (like rsync for cloud storage)
    - `filezilla` (ftp client)
    - `libnotify-bin` (enables you to create desktop notifications
      with `notify-send`)


44. [Gnome extensions](https://extensions.gnome.org)

    - (Can install, uninstall, and configure extensions within browser)
    - [Clipboard indicator](https://extensions.gnome.org/extension/779/clipboard-indicator)
      (gives clipboard history)
    - [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
    - [Audio Switcher](https://extensions.gnome.org/extension/1092/audio-switcher/)
    - [system-monitor](https://extensions.gnome.org/extension/120/system-monitor/)
      (also needed `sudo apt install gir1.2-gtop-2.0`, and to log out
      and back in again)
    - [emoji selector](https://extensions.gnome.org/extension/1162/emoji-selector/_
      (also did `sudo apt install fonts-emojione`)
    - [gtile](https://extensions.gnome.org/extension/28/gtile/) (tile
      windows with a grid)
        - select window you want to resize
        - use Super-Enter (on number key pad) to open gtile
        - click one corner position and then the other on the grid
        - esc to exit
    - [hide activities button](https://extensions.gnome.org/extension/744/hide-activities-button/)
    - [Refresh wifi connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
      (adds a refresh button to the wifi connection dialog)
    - [Media player indicator](https://extensions.gnome.org/extension/55/media-player-indicator/)


45. Install [Slack](https://slack.com/downloads/linux)

    - Downloaded `.deb` file; opened it from Chrome to install.

46. Install [Corebird](https://corebird.baedert.org/), twitter client

    - Just used _Pop shop_ (the software installer for
      [Pop!_OS](http://pop.system76.com/docs)

47. Installed [WINE](https://www.winehq.org/) and
    [PlayOnLinux](https://www.playonlinux.com/en/) in the same way as
    Slack and Corebird. Seems like if I use PlayOnLinux, I don't
    really need to have installed WINE. And it seems that Office365
    (Office 2016) can't be installed with either at this point, so
    I don't really have any use for these.

48. Set up backups

    - Install Deja Dup via "Pop Shop"

    - Used command-line program `gnome-disks` to change to name of my
      extra hard drive.

    - Set up Deja Dup for a daily backup of my home folder, ignoring
      the Downloads folder.

    - Ignore the folders `~/Dropbox` and `~/VirtualBox VMs`

49. Copy over music

    - Used `rsync`; issue of having spaces in paths, but can do like
      this (note the backslashes _and_ quotes):

      ```
      rsync -a "fig.local:Music/iTunes/iTunes\ Music/They\ Might\ Be\ Giants" .
      ```

    - In banshee: Tools -> Rescan Music Library

    - `.m4a` files seem to work just as well as `.mp3`

50. [autokey](https://github.com/autokey/autokey) is great, but after a day or so it seems to start
    using up 100% of a CPU. In short term, seems like I could just use
    a `cron` job to re-start it every evening.

    So I made a shell script with

    ```
    pkill autokey
    sleep 10
    autokey-gtk >& /dev/null &
    ```

    I then used `crontab -e` to add to my crontab file:

    ```
    0 2 * * * /bin/bash [path_to_shell_script]
    ```

51. VirtualBox and Windows + Office365
    See <https://www.extremetech.com/computing/198427-how-to-install-windows-10-in-a-virtual-machine>

    - Download Windows 10 from
      <https://www.microsoft.com/en-us/software-download/windows10ISO>
    - Download VirtualBox from
      <https://www.virtualbox.org/wiki/Downloads>
      - Add to `/etc/apt/sources.list`
      - Register Oracle public keys
      - `sudo apt install virtualbox-5.2`
      - `sudo apt install dkms`
    - Start `virtualbox`, create new Windows10 machine, adjust memory,
      disk size, connect to the windows ISO, and adjust display stuff
    - Then start the virtual machine to install windows10. I said I had
      no product key, chose Windows 10 Home edition, and said something
      like fresh install
    - The thing was deathly slow. Searched for solutions and found
      this: <http://blog.jdpfu.com/2012/09/14/solution-for-slow-ubuntu-in-virtualbox>

      - Followed these instructions, except for Network when I tried
        "Bridged" I didn't get a network connection so I switched back
        to the default "NAT" and that worked

      - Gave the machine 150 GB harddrive (dynamically sized) and 8192
        MB RAM. And went for 2 CPUs

      - Once windows was up and running, and changed the VM display to
        "scaled" and then within windows I changed the screen
        resolution to 1600x1200. Seems to work better.

    - Within Windows, installed Office365 (by going to office365.com
      and then logging in with my NetID from UW-Madison), R, Rtools,
      RStudio, and a bunch of R packages (devtools + tidyverse
      first)

    - Need to install "Guest additions". While the virtual box is
      running, you need the VirtualBox tool bar to be showing (it
      won't if you're using a "scaled" window, it seems). In the
      "Devices" menu there's an option to "insert guest additions
      CD". Then within windows, click on the CD and install the
      software.

    - Having installed the guest additions, you can share a linux
      folder with windows. First create a folder in your home
      directory that you will share. Then in VirtualBox settings, go
      to "Shared Folders" and right-click on "Machine Folders" and
      select "Add shared folder" and enter the path to the folder.

52. Was looking at finding a better linux terminal, but I think the
    standard gnome terminal will be fine for me.

    - Can open a new terminal in an additional tab with
      ctrl-shift-T
    - Switch between tabs with ctrl-PgUp and ctrl-PgDn
    - See all keyboard shortcuts by going to Edit -> Preferences ->
      Shortcuts

---

- Install ccache and use for compiling R

  - `sudo apt install ccache`
  - In `~/.R`:

- Additional possible gnome extensions:
  - [Places status indicator](https://extensions.gnome.org/extension/8/places-status-indicator/)
  - [Pomodoro timer](http://gnomepomodoro.org/)

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
