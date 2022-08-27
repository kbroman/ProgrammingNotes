## arduino

### arduino nano

I had a problem with an Arduino Nano on linux. It wouldn't show up as
connected. Tried various things with no luck, until [this one](https://stackoverflow.com/questions/70123431/why-would-ch341-uart-is-disconnected-from-ttyusb):

```shell
sudo apt remove brltty
```

Then also needed to do this:

```shell
sudo chmod a+rwx /dev/ttyUSB0
```

Then I also needed to choose "ATmega328P (Old Bootloader)" for "processor".

The way I found the solution was by googling the message that
showed up from `sudo dmesg`, namely

```
ch341-uart ttyUSB0: ch341-uart converter now disconnected from ttyUSB0
```
