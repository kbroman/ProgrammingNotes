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
   - Didn't seem to work for me, though.

9. Set up Apple magic mouse via bluetooth settings

   - It came up with a weird name; I had to go back to Mac and pair it
     and then rename it and then back to pair again with the linux
     laptop
   -

10. ssh keys + connect to github

   - [created new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
   - installed xclip with `sudo apt install xclip`
   - At github, settings -> ssh and gpg keys -> New SSH key
   - Tested it out by cloning `git clone git@github.com:kbroman/ProgrammingNotes`

9. Copy over stuff from my desktop

9. Get R and RStudio installed

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
