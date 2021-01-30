## Wifi networking diagnostics in linux


- Check network devices

  ```
  ifconfig -a
  ```

- Check wifi signal strength

  ```
  iwconfig
  iwconfig [wlan0] | grep -i signal
  ```

- command-line tool giving detailed info on wifi networks and signal
  strengths

  ```
  nmcli dev wifi
  ```
