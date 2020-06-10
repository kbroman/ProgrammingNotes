## Linux refresh

My galago pro laptop froze so I did a hard reboot but it wouldn't get
passed the decryption of the drive.

So I used a [live disk] of Pop!_OS 20.04 and "refreshed" the OS.
- insert USB stick with OS installed
- turn on while pressing F1
- choose firmware
- choose boot
- choose the USB
- then select to decrypt the drive and enter password
- then refresh the OS

This all worked fine, booted up normally, and all my personal stuff
was still there, but all programs are gone, so I did the following
slow reinstall

1. Update and upgrade

   ```shell
   sudo apt update
   sudo apt upgrade
   ```

2. Edit `/etc/hostname` and `/etc/hosts`
   - replace `popos` with what I want.
   - In `/etc/hostname`, it's just the one word
   - In `/etc/hosts`, it's on the line with `128.0.1.1`

3. emacs

   ```shell
   sudo apt install emacs
   ```

4. R

   ```shell
   sudo apt [whole bunch of libraries]
   sudo apt-key [blah blah blah]
   sudo apt r-base r-recommended
   ```

5. LaTeX

   ```shell
   sudo apt install texlive-full
   ```

6. node

   ```shell
   sudo apt install npm
   sudo npm install -g coffeescript yarn gistup babel-core uglify-js uglifycss
   ```

7. ruby

   ```shell
   sudo apt install ruby-dev
   sudo gem update
   ```

8. dropbox, from <https://dropbox.com/install-linux>

   ```shell
   sudo dpkg -i dropbox_2020.03.04_amd64.deb
   ```

9. simplenote, from <https://simplenote.com>

   ```shell
   sudo dpkg -i Simplenote-linux-1.17.0-amd64.deb
   ```

10. wanted to install `libgnome2-bin` for `gnome-open`, but it's no
    longer available. can instead use `xdg-open` which was already
    installed.  I have a shell script `start` that loops over command-line
    arguments to open multiple files

11. gnome tweaks

    ```shell
    sudo apt install gnome-tweak-tool
    ```

12. bunch of stuff

    ```shell
    sudo apt install cheese gpick enscript gv ubuntu-restricted-extras
    sudo apt install vlc calibre handbrake gitg mg neofetch
    sudo apt install pdftk imagemagick trash-cli clementine
    ```

13. libnotify (desktop notifications with notify-send)

    ```shell
    sudo apt install libnotify-bin
    ```

    Could do like `system('notify-send "R is done!"')` in R

13. inconsolata font

    ```shell
    sudo apt install fonts-inconsolata
    sudo fc-cache -fv
    ```

14. autokey

    previously needed `sudo add-apt-repository ppa:sporkwitch/autokey`
    but doesn't seem like it anymore

    ```shell
    sudo apt install autokey-gtk
    ```

15. keepassxc

    ```shell
    sudo add-apt-repository ppa:phoerious/keepassxc
    sudo apt install keepassxc
    ```

16. playback of DVDs

    ```shell
    sudo apt install libdvd-pkg
    sudo dpkg-reconfigure libdvd-pkg
    ```





---

to do:
- set up backups
- virtual box?
- tunnelbear
- eduroam
- globalprotect vpn
- libreoffice
- anaconda
- julia

- skype
- rstudio (+ link to pandoc in /usr/local/bin)
- chrome
- okular
- moneydance
- java
- Minecraft
