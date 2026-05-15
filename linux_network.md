## linux network commands

`ifconfig` is apparently deprecated

- view interfaces (`grep link` to get MAC addresses; `grep 192` to get
those with 192 IP)

  ```
  ip link
  ```

- view those with ip address

  ```
  ip a
  ```

- take `eth0` down

  ```
  sudo ip link set eth0 down
  ```

- bring `eth0` back up

  ```
  sudo ip link set eth0 up
  ```

- [Commands re setting static IP](https://www.abelectronics.co.uk/kb/article/31/set-a-static-ip-address-on-raspberry-pi-os-trixie)


  ```
  nmcli -o device show

  sudo nmcli -p connection show

  sudo nmcli c mod netscan-eth0 ipv4.addresses 192.168.50.11/24 ipv4.method manual
  sudo nmcli c mod netscan-eth0 ipv4.gateway 192.168.50.1
  sudo nmcli c mod netscan-eth0 ipv4.dns 192.168.50.1
  ```
