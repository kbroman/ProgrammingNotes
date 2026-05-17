## linux network commands

`ifconfig` is apparently deprecated

- view interfaces (`grep link` to get MAC addresses)


  ```
  ip link
  ```

- view those with ip address (`grep 192` to get those with 192 IP)

  ```
  ip a
  ```

- take `eth0` down and back up
  (want to do both, especially if accessing remotely

  ```
  sudo ip link set eth0 down && sudo ip link set eth0 up
  ```

- [Commands re setting static IP](https://www.abelectronics.co.uk/kb/article/31/set-a-static-ip-address-on-raspberry-pi-os-trixie)


  ```
  # show devices
  nmcli device

  # devices with full details
  nmcli device show

  # get DNS servers used
  nmcli device show | grep DNS

  # get DNS server for particular device
  nmcli device show eth0 | grep DNS

  # show connections
  nmcli connection show

  # set static IP
  sudo nmcli c mod netplan-eth0 ipv4.addresses 192.168.50.11/24 ipv4.method manual
  sudo nmcli c mod netplan-eth0 ipv4.gateway 192.168.50.1
  sudo nmcli c mod netplan-eth0 ipv4.dns 192.168.50.1
  ```
