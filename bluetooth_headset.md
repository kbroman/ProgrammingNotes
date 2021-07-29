## bluetooth headset

Here I discuss my futzing to get my airpods to work with Ubuntu.

The key thing seemed to be to switch from ad2p to hsp/hfp. And I guess
really hfp, since there's apparently not support for hsp.

1. Use [bluetooth
   manager](https://askubuntu.com/questions/831331/failed-to-change-profile-to-headset-head-unit/1236379#1236379)
   to pair with the airpods.

2. If you right-click on the airpods, you want to be able to select
   "Audio profile" and then choose "Headset Head Unit" (rather than
   "High fidelity playback")

3. Install ofono

   ```shell
   sudo apt install ofono
   ```

4. Configure pulseaudio to use ofono by editing
   `/etc/pulse/default.pa` so that the line

   ```
   load-module module-bluetooth-discover
   ```

   becomes

   ```
   load-module module-bluetooth-discover headset=ofono
   ```

5. Add the `pulse` user to the `bluetooth` group

   ```shell
   sudo usermod -aG bluetooth pulse
   ```

6. Add the following to `/etc/dbus-1/system.d/ofono.conf` (before
   `</busconfig>`):

   ```
   <policy user="pulse">
       <allow send_destination="org.ofono"/>
   </policy>
   ```

7. Install `ofono-phonesim`; I needed to add a ppa

   ```shell
   sudo add-apt-repository ppa:smoser/bluetooth
   ```

   Then I needed to edit `/etc/apt/sources.list.d/smoser-ubuntu-bluetooth-groovy.list`
   to change `groovy` (20.10) to `focal` (20.04).

   Then I could add `ofono-phonesim`:

   ```shell
   sudo apt install ofono-phonesim
   ```

8. Start an ofono modem

   ```shell
   ofono-phonesim -p 12345 /usr/share/phonesim/default.xml
   ```

9. Modify `/etc/ofono/phonesim.conf` to use it:

   ```
   [phonesim]
   Driver=phonesim
   Address=127.0.0.1
   Port=12345
   ```

10. Restart oFono:

   ```shell
   sudo service ofono restart
   ```

11. Then I could go back to the bluetooth manager, right-click the
    airpods, and select "Audio Profile" and then "Headset Head Unit".

12. After restarting my system, I needed to re-run the
    `ofono-phonesim` command, but then it still didn't work. I needed
    to clone ofono and run the script `enable-modem`:

    ```shell
    git clone git://git.kernel.org/pub/scm/network/ofono/ofono.git
    cd ofono/test
    ./enable-modem
    ```

The key sites that helped:
- <https://askubuntu.com/questions/985615/bluetooth-profile-locked-to-a2dp-high-quality-audio-sink-but-cannot-change-to/1223200#1223200>
- <https://askubuntu.com/questions/831331/failed-to-change-profile-to-headset-head-unit/1236379#1236379>
- <https://askubuntu.com/questions/1242450/when-will-add-ofono-phomesim-to-the-focal-repository-20-04>

- Sites I looked at previously:

  - [pulseaudio issue](https://gitlab.freedesktop.org/pulseaudio/pulseaudio/-/issues/81)
  - [askubuntu](https://askubuntu.com/questions/1085480/bluetooth-headphones-switches-from-a2dp-sink-to-hsp-hfp-when-starting-voip-a)
  - [another askubuntu question](https://askubuntu.com/questions/354383/headphones-microphone-is-not-working)

---

- airpods as headphones sound nice
- airpods as headset: seems like both the headphones and the mic are
  really crappy quality...not worth the trouble
- so best to just leave them as headphones
- but on galago pro, while I could pair and connect/disconnect
  airpods, I'm having trouble getting pulseaudio to recognize them
- what worked was [this answer]:
  - unpair the airpods
  - `sudo pkill pulseaudio`
  - re-pair the airpods
- upgrading to PopOS 20.10 fixed this problem
