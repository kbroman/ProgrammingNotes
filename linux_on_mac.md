

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

6. Get UW-Madison VPN working

   - download PanGPLinux-5.3.0-c32... from <https://www.net.wisc.edu/vpn/clients/>

   - extract

   - install the "UI" deb file

     ```
     sudo apt install libqt5webkit5
     sudo dpkg -i GlobalProtect_UI_deb-5.3.0.0-32.deb
     ```

   - it started up automatically; use `uwmadison.vpn.wisc.edu` as the portal
     and `broman_1` as the user name

7. Copy .bashrc from broster2 laptop

8. Copy wallpapers from broster2 laptop, in `~/Pictures/Wallpaper` and
   change background using Settings -> Desktop -> Background; then
   "Add Picture" and select it.

9. Test webcam by installing cheese (like photobooth on Mac)

   ```
   sudo apt install cheese
   cheese
   ```

10. Install zoom from within Pop!_Shop

11. Set up ssh + connect to github

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


---

9. Set up ssh

10. Set up git

11. Get gnome utilities installed

11. Install R

12. Install ESS and other emacs modes

13. Install Latex

14. Install Dropbox

15. Install SimpleNote

17. connect to printer

18. install google chrome

19. connect a usb stick

20. Install RStudio

21. Link to pandoc that shipped with RStudio

22. Okular pdf reader

23. additional packages

24. create "start" script that acts like "open" on a mac

25. get terminal to open at startup

16. Install Skype