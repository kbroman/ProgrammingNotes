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
     couldn't connect to BMI servers.

9. ssh keys + connect to github

   - [created new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   - installed xclip with `sudo apt install xclip`
   - At github, settings -> ssh and gpg keys -> New SSH key
   - Tested it out by cloning `git clone git@github.com:kbroman/ProgrammingNotes`
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
  - **FIX ME**: install a bunch more packages

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
    - **FIX ME**: shows up _really_ small when screen is in high-def mode
    - **FIX ME**: camera is not working yet


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

23. Okular pdf reader

    - `sudo apt install okular`
    - Installs a _ton_ of dependencies

---

- get the VPN to work

- copy other stuff into ~/.bashrc

- python3

- ruby

- npm and coffeescript

- VirtualBox and Windows + Office365

- Java

- Minecraft

- Backups (dejadup)

- clipman (or gpaste)

- caffeine

- autokey

- Change the wallpaper

- better terminal

- vlc

- get camera to work in skype

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
