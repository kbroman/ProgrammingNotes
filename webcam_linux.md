## Webcams in linux

(Personally, I've got a cheap Logitech C615 and a fancier C930e. Well,
plus a C920S which I'm getting to replace the C615.)

The main software to control the settings on these cameras is
`v4l2-ctl`. Here's a relevant [blog
post](https://www.kurokesu.com/main/2016/01/16/manual-usb-camera-settings-in-linux/)
and the [man page](https://www.mankier.com/1/v4l2-ctl)



- install software:

  ```
  sudo apt update
  sudo apt install v4l-utils
  ```

- list devices

  ```
  v4l2-ctl --list-devices

  # HD Webcam C615 (usb-0000:00:14.0-5.1.6):
  #   /dev/video0
  #   /dev/video1
  ```

- list controls

  ```
  v4l2-ctl -d /dev/video0 --list-ctrls
  ```

  Note: can also use `-d 0` or just leave that off if `/dev/video0`

  I'm most interested in `focus_auto` and `exposure_auto`

  ```
  v4l2-ctl -d /dev/video0 --set-ctrl=focus_auto=0
  v4l2-ctl -d /dev/video0 --set-ctrl=exposure_auto=1

  v4l2-ctl -d /dev/video0 --set-ctrl=white_balance_temperature_auto=0
  v4l2-ctl -d /dev/video0 --set-ctrl=white_balance_temperature=3200

  v4l2-ctl --set-ctrl=zoom_absolute=2
  ```

- list possible resolutions

  ```
  v4l2-ctl --list-framesizes=YUYV

  ```

- set resolution

  ```
  v4l2-ctl --set-fmt-video=width=960,height=720,pixelformat=YUYV
  ```

  I can't really see whether this works

---


## GUI guvcview

I also added guvcview via pop-shop; it gives the same control with a
GUI and with ability to preview what you're doing.
