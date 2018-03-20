## Linux on a chromebook

Got an [Acer Chromebook
14](https://www.amazon.com/gp/product/0387921249?ie=UTF8&tag=7210-20)
with 1920x1080 screen, 4 GB RAM, and 32 GB SSD (says model number
CB3-431; chromeOS model `EDGAR D25-E5K-S8I-A85`)

### Some links

- [lifehacker](https://lifehacker.com/how-to-install-linux-on-a-chromebook-and-unlock-its-ful-509039343)
- [softpedia](http://news.softpedia.com/news/how-to-install-ubuntu-17-04-with-gnome-on-your-chromebook-alongside-chrome-os-516624.shtml)
- [Jenny Bryan](https://github.com/jennybc/operation-chromebook)

### General procedure

- Put into recovery mode (esc-refresh-power)

- ctrl-D to put in developer mode

- ctrl-alt-T to open a terminal, then type `shell` in the terminal

- download [crouton](https://github.com/dnschneid/crouton)

- list options: (`-r` = distros; `-t` = desktops)

  ```shell
  sh ~/Downloads/crouton -r list
  sh ~/Downloads/crouton -t list
  ```

- Install crouton (`-e` to encrypt)

  ```shell
  sh ~/Downloads/crouton -e -r xenial -t gnome
  ```

- Use `sudo startgnome` to start the desktop

- Note that the "search" key acts as a super key

### Install stuff

- set locale

  ```shell
  sudo locale-gen "en_US.UTF-8"
  sudo dpkg-reconfigure locales
  ```

- `sudo install emacs mg gnome-terminal`

- Follow [Jenny's instructions](https://github.com/jennybc/operation-chromebook) to get R and RStudio
