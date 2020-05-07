## Linux tricks

- change title in a terminal

  ```
  echo -e '\033]2;Some Title\007'
  ```

  (see [this stackexchange entry](https://unix.stackexchange.com/a/358986))


- Direct ethernet connection between laptops

  - Issue is that you don't have DNS

  - Open Network preferences and create a Wired profile that just has,
    under IPv4, IP `192.168.0.1` on one computer and `192.168.0.2` on
    the other. Use Netmask `255.255.255.0` on both.

  - Should then be able to `scp` between them.

  - Main problem I had is that the cable I was using was bad; switched
    cables and it worked.
