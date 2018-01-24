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

9. Set up Apple magic mouse via bluetooth settings

   - It came up with a weird name; I had to go back to Mac and pair it
     and then rename it and then back to pair again with the linux
     laptop
   - Scrolling speed was deathly slow. Followed instructions
     at <https://askubuntu.com/a/262730>. In particular, I used:

     ```
     options hid_magicmouse scroll-speed=60 scroll-acceleration=2
     ```
   - **FIX ME**: want scrolling to go in the opposite direction

10. ssh keys + connect to github

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

11. Copy over stuff from my desktop

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
      
12. Set up mail in Geary

    - First tried setting up gmail; authentication didn't work
    - Needed to create an App-specific password; see
      <https://support.google.com/accounts/answer/185833>


13. Install R

   - See [instructions at digitalocean](https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-16-04-2)

   ```
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
   sudo add-apt-repository 'deb https://cran.rstudio.com/bin/linux/ubuntu artful/'
   sudo apt update
   sudo apt install r-base
   ```

14. Install RStudio

10. Install ess

11. python, ruby, coffeescript

12. Connect to mail (maybe drop geary and use thunderbird)

13. Install skype and dropbox

14. Install LaTeX (texlive)

15. Install SimpleNote

16. Install VirtualBox and Windows + Office365

17. Install Java and Minecraft

18. Backups

19. clipman, caffeine, autokey

7. Change the wallpaper
