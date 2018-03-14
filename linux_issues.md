## Linux issues


- Having trouble with displays. In particular, getting the right
  setting on my external display, and having it work on its own,
  with the laptop's display off. Even better would be to use it with
  the laptop closed.

  The thing that seems to work: log in, select display settings (to
  have external display as single monitor), then close laptop (to
  suspend), then open laptop again

- Emoji fonts don't seem to work. For example, using them with
  autokey. Can paste them normally (though black-and-white) but they
  don't show up within autokey

- VPN not working with eduroam, though it does work with wired
  ethernet connection. Actually, a week later it seemed to work. Not
  sure why.

- warnings etc from okular

  ```
  Icon theme "breeze" not found.
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/16/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/22/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/24/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/32/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/48/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/64/"
  Invalid Context= "stock" line for icon theme:  "/usr/share/icons/ubuntu-mono-dark/stock/128/"
  Icon theme "Mint-X" not found.
  Icon theme "elementary" not found.
  Illegal icon group:  7
  ```

- Apple bluetooth magic mouse and magic trackpad

- Periodic troubles logging in, with a spinning circle and then a
  message "Authentication error" repeat some number of times.
  Sometimes it ends up logging in, sometimes repeats a ton of times so
  I eventually restart at which point all is fine.

  - System 76 suggested re-installing the login manager, gdm3

    ```shell
    sudo apt install --reinstall gdm3
    ```
