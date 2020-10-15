## bluetooth headset

- getting the microphone to work:

  Edit `/etc/pulse/default.pa` so that the line
  with `load-module module-bluetooth-policy` ends with `auto_switch=2`

- Trying to switch from ad2p to hsp/hfp (or something like that)

  Never did get it to work

- Sites I looked at:

  - [pulseaudio issue](https://gitlab.freedesktop.org/pulseaudio/pulseaudio/-/issues/81)
  - [askubuntu](https://askubuntu.com/questions/1085480/bluetooth-headphones-switches-from-a2dp-sink-to-hsp-hfp-when-starting-voip-a)
  - [another askubuntu question](https://askubuntu.com/questions/354383/headphones-microphone-is-not-working)
