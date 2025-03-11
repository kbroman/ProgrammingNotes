## Thunderbolt

- Trying to get two Dell U2725QE displays working with my System76
  laptops via thunderbolt


### Old Galago Pro (galp3-c)

- This has only thunderbolt3 (not 4) so it won't be able to run both
  4k displays when chained.

- But it does do thunderbolt on the first display (both running the
  display and charging the laptop), and grabs the
  signal for USB accessories from *both*.
  (My mouse, keyboard, and webcam are connected to the first display;
  my headset is connected to the second.)

- Connected the second display via HDMI. The first display (connected
  via thunderbolt3) is at 60 Hz, and the 2nd (via HDMI) is at 30 Hz.

- This laptop doesn't use system76's new open firmware. So I had to go
  into the BIOS (restart laptop while holding down ESC) and, under
  "Advanced", enable
  thunderbolt, changed the security level for the thunderbolt port,
  and in Advanced Chipset Control -> DDI Control, use DDI to TBT
  (rather than DDI to mDP)

- In Settings, search for Thunderbolt, which shows both displays when
  they're connected

### Darter Pro (darp8)

- Still haven't gotten this to work. Rather than BIOS, it uses the
  newer System76 Open Firmware, but I don't see how to access firmware
  settings.
