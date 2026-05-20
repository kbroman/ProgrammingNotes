## PopOS on a thinkpad

I got an old thinkpad T14S (gen 2i) and want to install PopOS on it.

1. Made a bootable USB drive with PopOS 24.04

2. Windows prep

   - with a bit of effort, got my windows product key (just in case);
     went to [this site](https://support.lenovo.com/us/en/solutions/ht500032-how-to-find-the-windows-7-product-key_)
     and entered my serial number; then scrolled down to the case that
     I don't have a Windows label. There was a VB script to save with
     in a file on the desktop; double-click that and the product key
     was shown

   - Turned off Fast Startup: search for "choose a power plan" and
     then select "choose what the power button does". Then "Change
     settings that are currently unavailable" so that I can then
     de-select "turn on fast start"

   - Turn off bitlocker (drive encryption): search "manage bitlocker"
     and then "turn off bitlocker"

3. Shrink windows disk

   - search "computer management"
   - select "Disk management"
   - right-click the c: drive and click "shrink value"
   - select an amount to make the disk 50:50

4. Create new partition for linux

   - right-click the unallocated space and select "New simple volume"
   - I chose "Do not assign a drive letter"
   - format as NTFS
   - gave it the name "Linux"

5. Enable boot from USB

   - Restart computer and press F12 at the splash screen

   - Choose "app menu" and "Security" and then "Secure Boot"

   - Looking for an option "Allow Microsoft 3rd Party UEFI CA"
     but it wasn't there. Instead de-selected "Secure boot";
     that seemed to work

6. Re-start again, and again press press F12 when the splash screen
   comes up

   - Click on USB HDD

   - PopOS screen! Clock "try or install..."

7. Installing PopOS

   - A bunch of simple questions about language etc

   - Choose "Custom" (rather than "Clean Install")

   - It doesn't make it easy to know which partition to use, but
     selecting "modify partitions" it shows you the partitions and
     labels, so for me it was clear that Linux went with `/dev/nvme0n1p4`

   - Turns out that I needed space for swap, so I went back to
     "Modify partitions" and gave ~17 GB for swap plus ~200 MB empty
     right before the linux partition

   - It didn't seem I had enough space for the EFI partition, so I
     went back and shrunk the main linux one again, so there was ~2 GB
     space for EFI. But I probably just needed 1 GB for the EFI partition.

   - Was then able to create a user and install PopOS

   - Went back to BIOS setup: F12 -> App Menu -> Setup -> Security ->
     Secure Boot -> re-selected Secure Boot

   - Then Startup -> Boot and then edit boot order

   - I went back again to try to disable "secure boot"
     since it wouldn't seem to let me boot PopOS, but the "Security"
     option was gone.

   - tried restarting and pressing enter and F1, which seems to be
     another way to get in to the BIOS settings, and the "Security"
     option was back, so de-selected secure boot and restarted

   - ...and it booted into PopOS 😊

8. The location of the ctrl key was killing me...kept pressing Fn
   instead. Apparently that is a common problem, as there is a BIOS
   setting to swap them.

   - Re-start and press F12, then Apps, Settings, Config, Keyboard,
     Swap Fn and Ctrl keys

9. Set up fingerprint sensor; see
   <https://hackeradam.com/enable-fingerprint-authentication-on-popos/>

   ```
   sudo apt install fprintd libpam-fprintd
   fprintd-enroll # (then touch the fingerprint sensor repeatedly)
   sudo pam-auth-update
   ```

   Use `fprintd-verify` to check that it works

   Doesn't seem to work at login, but does work as authentification
   for `sudo`; just gives you one chance to get it right, though.

   ...but later (after a couple of reboots?) it did just ask for
   fingerprint at login

9. After futzing around with Windows, trying to install a Minecraft
   server directly and via docker, I wanted to re-install windows to
   start fresh and try it all again.

   - The bootable USB with Windows that I'd created from my PopOS
     computer didn't work...the thinkpad refused to boot from it.

   - So created a bootable USB for Windows 11 from within Windows on
     the thinkpad.  I went to the [Windows 11 download
     site](https://www.microsoft.com/en-us/software-download/windows11)
     and clicked on "Download Now" under the section "Create Windows
     11 Installation Media". That downloads an application that you
     can run to create the bootable USB.

   - Then went though similar process as installing Linux: reboot and
     press F12 and then selection the USB, and you get into the
     Windows Installation. Just need to select the Windows partition.

   - Initially the touchpad didn't work, but "pointing stick" worked,
     and once Windows was up and running again, the touchpad worked
     again. Plus it turns out that this Thinkpad also has a touch
     screen.
