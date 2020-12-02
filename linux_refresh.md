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
   sudo apt install [whole bunch of libraries]
   sudo apt install libudunits2-dev libmagick++-dev
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
   sudo apt --fix-broken install
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
    sudo apt install ccache openssh-server htop
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

17. LibreOffice

    ```shell
    sudo apt install libreoffice
    sudo apt install okular
    ```

18. [moneydance](https://infinitekind.com/download-moneydance-personal-finance-software)

    ```shell
    sudo dpkg -i moneydance_linux_amd64.deb
    ```

19. [Chrome](https://www.google.com/chrome/browser/desktop/index.html)

    ```shell
    sudo dpkg -i google-chrome-stable_current_amd64.deb
    sudo apt --fix-broken install
    ```

20. [RStudio](https://rstudio.com/products/rstudio/download/#download)
    (check file download with `sha256sum`)

    ```shell
    sudo apt install libclang-dev
    sudo dpkg -i rstudio-1.3.959-amd64.deb
    ```

21. Set up backups

    - Install Deja Dup via "Pop Shop"

    - Folders to save: "Home (kbroman)"

    - Folders to ignore: `Downloads`, `Dropbox`, `ISOs`, and
      `~/VirtualBox VMs`.

    - Storage Location: Local Folder,
      `/media/kbroman/Broster2Backup/kbroman_backup`

    - Needed to enter decryption password for Deja Dup
      (see keepassxc)

    - complaint about "broster2" vs "broster2.localdomain", but it
      seemed to work

22. Tunnelbear

    - `sudo apt install network-manager-openvpn-gnome`
    - previous configuration files were already there

24. Globalprotect vpn

   - Download and extract `PanGPLinux-[version].tgz` from <https://www.net.wisc.edu/vpn/clients/>.
   - This gives a `GlobalProtext_deb-[version].deb` file, to install via
     `sudo dpkg -i GlobalProtect_deb-*.deb`.
   - First time, use `globalprotect connect --portal uwmadison.vpn.wisc.edu`
   - Then use `globalprotect connect` and `globalprotect disconnect`.
   - Use NetID and password; use `[username]_1` for static IP.

25. Skype

    - Download `.deb` file from <https://www.skype.com/en/get-skype/>
    - Install with `sudo dpkg -i skypeforlinux-64.deb`

26. Zoom

    - Download `.deb` file from <https://zoom.us/download>
    - `sudo dpkg -i zoom_amd64.deb`
    - Needed to install libegl1-mesa, libgl1-mesa-glx, libxcb-xtest0;
      accomplished with `sudo apt --fix-broken install`

27. Julia

    - downloaded the `.tar.gz` file with "generic linux
    binaries", from <https://julialang.org/downloads/>

    - extracted into `/usr/local/`

    - created symbolic link to `/usr/local/src/julia-1.5.3/bin/julia`
      in `/usr/local/bin`

    - ran `julia` and installed IJulia to enable use in jupyter
      notebooks

      ```
      using Pkg
      Pkg.add("IJulia")
      ```

      then when running `jupyter notebook`, can click "New" and the
      options are both "Python3" and "Julia1.1.1"

---

to do:
- virtual box?
- eduroam
- java
- Minecraft

---

No need

- Conda was installed in `~/.anaconda3` so still there and working
- pandoc was installed with conda
