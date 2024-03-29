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
   sudo apt install qpdf
   sudo apt install libgit2-dev
   sudo apt install devscripts
   sudo apt-key [blah blah blah]
   sudo apt install r-base r-recommended
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

14. espanso (much better than autokey); customizations in `~/.config/espanso/default.yml`

    ```shell
    sudo apt install libnotify-bin
    sudo apt install snapd
    sudo snap install espanso --classic
    espanso start
    ```

15. playback of DVDs

    ```shell
    sudo apt install libdvd-pkg
    sudo dpkg-reconfigure libdvd-pkg
    ```

16. LibreOffice

    ```shell
    sudo apt install libreoffice
    sudo apt install okular
    ```

17. [moneydance](https://infinitekind.com/download-moneydance-personal-finance-software)

    ```shell
    sudo dpkg -i moneydance_linux_amd64.deb
    ```

18. [Chrome](https://www.google.com/chrome/browser/desktop/index.html)

    ```shell
    sudo dpkg -i google-chrome-stable_current_amd64.deb
    sudo apt --fix-broken install
    ```

19. [RStudio](https://rstudio.com/products/rstudio/download/#download)
    (check file download with `sha256sum`)

    ```shell
    sudo apt install libclang-dev
    sudo dpkg -i rstudio-1.3.959-amd64.deb
    ```

20. Set up backups

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

    - Also want to have the drive mounted automatically. I found [this
      post at
      techrepublic](https://www.techrepublic.com/article/how-to-properly-automount-a-drive-in-ubuntu-linux/)
      helpful.

      - `sudo fdisk -l` to find the drive

      - `sudo blkid` to get the UUID for the drive

      - add line to `/etc/fstab`

        ```
        UUID=[blah blah] /media/kbroman/Broster2Backup auto nosuid,nodev,nofail,x-gvfs-show 0 0
        ```

      - verify fstab with `sudo mount -a`

21. Tunnelbear

    - `sudo apt install network-manager-openvpn-gnome`
    - previous configuration files were already there, but needed to
      make use of them
    - Open Network settings; click plus sign by VPN and choose "Import
      from file"
    - needed to right-click and show hidden files, then navigated to
      `.tunnelbear_config/openvpn` and selected a file and clicked "Add"
    - need to open config and add tunnelbear email and password
      under "identify" tab

22. Globalprotect vpn

   - Download and extract `PanGPLinux-[version].tgz` from <https://www.net.wisc.edu/vpn/clients/>
   - This gives a `GlobalProtext_UI_deb-[version].deb` file, to install via
     `sudo dpkg -i GlobalProtect_UI_deb-*.deb`.
   - Use `globalprotect launch-ui`
   - Use NetID and password; use `[username]_1` for static IP.
   - type `1` to have it push a DUO verification to your phone


24. Zoom

    - Download `.deb` file from <https://zoom.us/download>
    - `sudo dpkg -i zoom_amd64.deb`
    - Needed to install libegl1-mesa, libgl1-mesa-glx, libxcb-xtest0;
      accomplished with `sudo apt --fix-broken install`
    - decided to remove those with `sudo apt remove zoom` and `sudo
      apt autoremove` and then install via "pop shop", but then needed
      to edit `~/.config/zoomus.conf` to have `autoScale=false`
      (otherwise, text in the GUI was super small, for example chat
      was nearly unreadable)

25. Julia

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

26. [Gnome extensions](https://extensions.gnome.org)

    - audio switcher 40 by albertomosconi
    - clipboard indicator by Tudmotu
    - emoji selector by Maestroschan
    - gTile by scherepanov
    - OpenWeather by jens
    - system-monitor by Cerin

    For audio switcher, said it was not compatible with latest version
    of gnome, but was able to install via [its github
    repository](https://github.com/AndresCidoncha/audio-switcher), and
    it seems to work fine. Cloned the repository into
    `~/.local/share/gnome-shell/extensions/audio-switcher@AndresCidoncha` and then restarted
    `gnome-shell` and it showed up. Actually, I needed to edit
    `metadata.json` to include `"42"` among the `"shell-version".

    The same is true for
    [system-monitor](https://github.com/paradoxxxzero/gnome-shell-system-monitor-applet/releases)
    and
    [emoji selector](https://github.com/maoschanz/emoji-selector-for-gnome);
    can manually install them by downloading/installing from github and
    then editing the metadata.json file

27. Gnome extensions: for system-monitor, needed:

    ```shell
    sudo apt install gir1.2-gtop-2.0 gir1.2-nm-1.0 gir1.2-clutter-1.0
    ```

    As above for audio switcher 40, had to do a bit more work to
    install this, since it's not been updated for Gnome 42.

    - Downloaded [zip file from
      GitHub](https://github.com/paradoxxxzero/gnome-shell-system-monitor-applet/releases).
    - extracted, entered directory, and typed `make install`
    - went to its directory in
      `~/.local/share/gnome-shell/extensions/...` and edited the
      `metadata.json` file to include `"42"` as one of the values for
      `"shell-version"`.

    In the preferences, deselected "Display icon" and selected "show
    tooltip", "move the clock", and "disply in the middle".

    De-selected "Display" in the "Net" tab, and de-selected "Show
    text" in the "Cpu" and "Memory" tabs.



28. Ability to connect to USB drive attached to a router

    ```shell
    sudo apt install smbclient exfat-fuse exfat-utils
    ```

    Add to `[global]` section of `/etc/samba/smb.conf`:

    ```
    client min protocol = CORE
    ```

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
