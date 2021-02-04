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

- wavemon - real-time version with info like `nmcli`, of wifi networks
  and signal strengths; can't figure out how to exit it -- F10 doesn't
  seem to work


- linssid - similar more graphic version of wavemon

- fast (`sudo snap install fast`): gives download speed using
  Netflix's speed testing service, <https://fast.com>

- speedtest (`sudo apt install speedtest-cli`): upload and download speed
  (using Ookla speedtest.net; see <https://www.speedtest.net/apps/cli>)

---

Apple has useful [suggestions on router
settings](https://support.apple.com/en-us/HT202068).
