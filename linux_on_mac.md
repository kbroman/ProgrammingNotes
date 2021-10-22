## Pop!_OS Linux on a Mac Pro

I have a Mac Pro desktop (mid 2012) where the MacOS can't be upgraded
anymore, so upon advice from Twitter, I'm installing linux on it. In
particular, I'm installing System76 Pop!_OS 21.04.

1. Initial software install

   - download Pop!_OS and install .ico onto USB thumb drive (I did this at home on a linux laptop using Popsicle)

   - shutdown Mac; insert USB drive; turn on while holding option key

   - select "EFI boot"

   - choose to install Pop_OS; erase and clean install; identify appropriate drive

2. Update either within Pop!_Shop or

   ```
   sudo apt update
   sudo apt upgrade
   ```

3. Had troubles with one of my displays. I have two Apple Cinema
   Displays, 2560x1600; one connected via DVI and the other with mini
   display port. The mini display port one (recognized as "Display 1"
   but I make it non-primary) works on start up but then goes
   black. Turning it off and on again didn't help, but unplugging the
   display port and plugging it back in again did. (It also has a DVI
   cable, but with a DVI to display port adapter, because my graphics
   card has just one DVI input.

4. Change mouse setting to "natural scrolling"

5. Install `mg` and `emacs`

   ```
   sudo apt install mg
   sudo apt install emacs
   ```

6. Install 1password; download from <https://1password.com/downloads/linux/>

   ```
   sudo dpkg -i ~/Downloads/1password-latest.deb
   sudo apt --fix-broken install
   ```

7. Get UW-Madison VPN working

   - download PanGPLinux-5.3.0-c32... from <https://www.net.wisc.edu/vpn/clients/>

   - extract

   - install the "UI" deb file

     ```
     sudo apt install libqt5webkit5
     sudo dpkg -i GlobalProtect_UI_deb-5.3.0.0-32.deb
     ```

   - it started up automatically; use `uwmadison.vpn.wisc.edu` as the portal
     and `broman_1` as the user name

8. Copy .bashrc from broster2 laptop

9. Copy wallpapers from broster2 laptop, in `~/Pictures/Wallpaper` and
   change background using Settings -> Desktop -> Background; then
   "Add Picture" and select it.

10. Test webcam by installing cheese (like photobooth on Mac)

    ```
    sudo apt install cheese
    cheese
    ```

11. Install zoom from within Pop!_Shop

12. Set up ssh + connect to github

   - [created new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   - installed xclip with `sudo apt install xclip`
   - also installed xsel with `sudo apt install xsel`
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


13. [Gnome extensions](https://extensions.gnome.org)

    - install utility for system-monitor

      ```
      sudo apt install gir1.2-gtop-2.0 gir1.2-nm-1.0 gir1.2-clutter-1.0 gnome-system-monitor
      ```
    - audio switcher by Gwynbleid94
    - clipboard indicator by Tudmotu
    - emoji selector by Maestroschan
    - gTile by scherepanov
    - OpenWeather by jens
    - system-monitor by Cerin
    - turn off Pop Shell (using GTile instead); seems like you need to do this from the application `gnome-extensions`


14. Install slack, discord, skype, dropbox, simplenote, okular, clementine, libreoffice from Pop!_Shop

    - seemed like I had to do something else to get dropbox running in the background, but I'm not sure what I did

15. Keyboard shortcuts

    Launchers/launch calculator: super+c
    Navigation: move window one monitor to left: shift+super+left
    Navigation: move window one monitor to right: shift+super+right
    Navigation: move window one workspace down: shift+super+down
    Navigation: move window one workspace up: shift+super+up
    Screenshots: Save a screenshot of an area: shift+alt+P

16. Install various utilities

    neofetch (command-line system info)
    gnome-tweak-tool
    gpick gv ubuntu-restricted-extras vlc calibre enscript
    handbrake gitg pdftk imagemagick trash-cli ccache openssh-server htop

17. Install `libnotify-bin` (needed by espanso, plus it enables you to
    create desktop notifications with `notify-send`; so in R you
    could do like `system('notify-send "R is done!"')`)

    ```
    sudo apt install libnotify-bin
    ```


17. Install [espanso](https://espanso.org) (*much* better than autokey) for text expansion;
    customizations in `~/.config/espanso/default.yml`

    ```
    sudo apt install snapd
    sudo snap install espanso --classic
    espanso start
    ```

18. Install R

    - Install a bunch of linux stuff

      ```shell
      sudo apt install --no-install-recommends software-properties-common dirmngr
      sudo apt install xauth xorg libx11-dev openbox
      sudo apt install libglu1-mesa-dev libfreetype6-dev
      sudo apt install libtiff-dev libfftw3-dev
      sudo apt install gfortran-9 libgdal-dev libproj-dev
      sudo apt install libcurl4-openssl-dev libssl-dev
      sudo apt install libxml2-dev libssh2-1-dev
      sudo apt install libblas-dev liblapack-dev gfortran
      sudo apt install libgit2-dev
      sudo apt install devscripts
      sudo apt install libjpeg62
      ```

    - Set up secure apt; see instructions at <https://cran.r-project.org/bin/linux/ubuntu/#install-r>

      ```
      wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
      sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
      ```

    - Install R

      ```
      sudo apt install --no-install-recommends r-base
      ```

19. Direct-connect computers via ethernet

    - My Mac Pro has a second ethernet port, which I'm using to directly connect to a laptop
    - On Mac Pro in Network settings, there are separate lines for the two ethernet jacks; for the jack of interest:
      - changed the name under "Identity"
      - Under IPv4, selected "Manual" and entered address 10.0.0.1 and netmask 255.255.255.0 and de-selected DNS
    - On my linux laptop in Network settings, I clicked "+" next to "Wired" to add another profile
      - changed the name under "Identify"
      - Under IPv4, selected "Manual" and entered address 10.0.0.2 and netmask 255.255.255.0 and de-selected DNS

20. Copy ssh keys between desktop and laptop

21. Install npm and coffeescript

    - `sudo apt install npm`
    - `sudo npm install -g coffeescript`
    - `sudo npm install -g yarn`

    Also [`gistup`](https://github.com/mbostock/gistup):

    - `sudo npm install -g gistup`

22. Install ruby

    - `sudo apt install ruby-dev` (gives version 2.3.3; close enough?)

23. Install python-dev

    - `sudo apt install python3-dev`


24. Install ESS and other emacs modes

    - ess downloaded from <https://ess.r-project.org> and placed in `~/.emacs.d/site-lisp`
    - install other packages using [Melpa](https://melpa.org):

      - include some stuff in `~/.emacs` file

      - `M-x package-refresh-contents` and then `M-x package-install`
        and name of package: markdown-mode,

        ```
        haskell-mode
        magit
        coffee-mode
        psci (purescript repl)
        d-mode
        markdown-mode
        inf-ruby
        json-mode
        ```

25. Install LaTeX (texlive)

    - I just did plain `sudo apt install texlive-full`


26. create "start" script that acts like "open" on a mac; need `xdg-open`

    ```
    sudo apt install xdg-utils
    ```

    the bash script (in `~/.local/bin/start`):

    ```bash
    for file in "$@"
    do
        xdg-open "$file" >& /dev/null  # ">& /dev/null" to suppress all warnings
    done
    ```

27. connect to printer (it happened automatically, somehow)

28. connect a usb stick (in just worked, in `/media/kbroman/[volume name]`)

29. Install Google Chrome

    - Download from <https://www.google.com/chrome/browser/desktop/index.html>
    - Install libappindicator1 with `sudo apt install libappindicator1`
    - Install chrome with `sudo dpkg -i google-chrome-*.deb`

30. Install RStudio

    - Download from <https://www.rstudio.com/products/rstudio/download/#download>
    - `sudo apt install libclang-dev libpq5`
    - Install with `sudo dpkg -i rstudio*.deb`

31. Install Inconsolata font

    ```
    sudo apt install fonts-inconsolata
    sudo fc-cache -fv
    ```
32. deja dup + set up backups

    - Install Deja Dup via "Pop Shop"

    - Folders to save: "Home (kbroman)"

    - Folders to ignore: `Downloads`, `Dropbox`, `ISOs`,
      `~/VirtualBox VMs`, `.zoom`

    - Storage Location: Local Folder,
      `/media/kbroman/figBackup/kbroman_backup`

    - Needed to enter decryption password for Deja Dup

33. Tunnelbear

    - `sudo apt install network-manager-openvpn-gnome`
    - copy over configuration files from
      `~/.tunnelbear_conofig/openvpn` on another computer
    - Open Network settings; click plus sign by VPN and choose "Import
      from file"
    - needed to right-click and show hidden files, then navigated to
      `.tunnelbear_config/openvpn` and selected a file and clicked "Add"
    - need to open config and add tunnelbear email and password
      under "identify" tab

---


20 Install docker

21. Link to pandoc that shipped with RStudio

25. get terminal to open at startup

27. Julia

34. playback of dvds

37. conda, python3
