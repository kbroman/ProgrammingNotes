## Creating a Mac High Sierra VM on Ubuntu

I got a [System76 Oryx Pro
laptop](https://system76.com/laptops/oryx) running
[Pop!_OS](https://system76.com/pop) (which is basically Ubuntu). I
want to run Mac OS X within [VirtualBox](https://www.virtualbox.org).

Initially I tried to install Mac Sierra
following notes at
[`suzywu2014.github.io`](http://suzywu2014.github.io/ubuntu/2017/02/23/macos-sierra-virtualbox-vm-on-ubuntu)

But I was getting errors, so I switched to following the primary source,
[`geerlingguy` at GitHub](https://github.com/geerlingguy/macos-virtualbox-vm).

But I was getting errors there, too. And I saw [this issue](https://github.com/geerlingguy/macos-virtualbox-vm/issues/24)
that the latest Sierra installer doesn't seem to work.

So I then switched to trying to install High Sierra, using instructions from
[`tobiwashere.de`](http://tobiwashere.de/2017/10/virtualbox-how-to-create-a-macos-high-sierra-vm-to-run-on-a-mac-host-system/)

But I got further errors. Or at least it seemed so.

Finally, I tried the
[tutorial at `howtogeek.com`](https://www.howtogeek.com/289594/how-to-install-macos-sierra-in-virtualbox-on-windows-10/)
even though the description concerns Windows 10. I think maybe the key advance
is that they mention the long, slow, scrolling text that look like
errors. "Don't worry about it. It's normal." They also select the
generic "Mac OS X (64-bit)" rather than the "High Sierra" version
(though I'm not sure if it matters, I stuck with it.)

1. On Mac, download Sierra installer from
   <https://itunes.apple.com/us/app/macos-sierra/id1127487414?ls=1&mt=12>

   Wait that's left over from when I was trying to install Sierra. For
   High Sierra, it will be easy to find the installer at the Mac App
   store, and you may already have a copy of the installer sitting in
   `/Applications`. (My Mac is still running Sierra and it's been
   pleading with me to upgrade for months.)

2. Also on Mac, prepare the High Sierra installer as an ISO

   ```
   hdiutil create -o /tmp/HighSierra -size 8G -layout SPUD -fs HFS+J -type SPARSE
   hdiutil attach /tmp/HighSierra.sparseimage -noverify -mountpoint /Volumes/install_build
   sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/install_build
   hdiutil detach /Volumes/Install\ macOS\ High\ Sierra/
   hdiutil convert /tmp/HighSierra.sparseimage -format UDTO -o /tmp/HighSierra.iso
   mv /tmp/HighSierra.iso.cdr ~/Desktop/HighSierra.iso
   rm /tmp/HighSierra.sparseimage
   ```

3. On Ubuntu, open virtual box and create a new VM

   ```
   name: MacVM
   MacVM: OSX
   version: Mac OS X (64-bit)
   RAM: 8192 GB
   Create a virtual hard disk (VDI; dynamic): 150 GB
   Pointing device: USB multi-touch tablet
   Select "Enable EFI" (I initially de-selected but got error)
   Processor: 2, with PAE/NX enabled
   Acceleration:
     paravirtualization interface: default
     Enable VT-x/AMD-V
     Enable Nested Paging
   Display: 128 MB Video Memory, Scale Factor 200%
   Shared Folders: Machine Folder to /home/kbroman/MacShare
   ```

   Also, load the `HighSierra.iso` into the virtual CD:

   - Open Settings for the MacVM in VirtualBox
   - Click on Storage
   - Click on the CD drive
   - Click the disk on the far right and select "Choose Virtual
     Optical Disk File" and select the `HighSierra.iso` file


4. **Close VirtualBox**, and on the command line:

   ```
   VBoxManage modifyvm "MacVM" --cpuidset 00000001 000306a9 04100800 7fbae3ff bfebfbff
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "MacBookPro11,3"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Mac-2BD1B31983FE1663"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
   ```

5. Install High Sierra by opening virtual box and starting the VM.

6. Don't panic.

7. Select language, then Disk Utility, then "Show All Devices", then
   Erase the "VBOX HARDDISK Media". Then close Disk Utility and
   select "Install macOS".

8. Shut down the VM, go into VirtualBox, eject the virtual CD, and
   restart the VM.

9. You get to the "`UEFI`" ugliness. Type:

   ```
   fs1:
   cd "macOS Install Data"
   cd "Locked Files"
   cd "Boot Files"
   boot.efi
   ```

10. Long, slow ugliness, then nice-looking Mac install. Then more
    ugliness. Again, don't panic.

11. Finally get to the "Welcome" page. Sigh. We made it.

12. Install stuff: iterm2, R, RStudio, command-line developer tools,
    Office 365, [gfortran](http://gcc.gnu.org/wiki/GFortranBinaries#MacOS)

13. VirtualBox doesn't have "Guest Additions" for Mac VM, so you can't
    do shared folders like you can with windows. But I'm able to
    `ssh`/`scp` from linux host to the Mac VM by doing the following:

    - Changed the Network setting for the Mac VM in VirtualBox from
      "NAT" to "Bridged adaptor"
    - On the Mac VM, went to Sharing Preferences and turned on "File
      Sharing" and "Remote Login", and gave the guest the name "MacVM"
    - Now can `ssh`/`scp` from linux host to `MacVM.local`.
    - **But** I don't have internet access with the bridged adaptor;
      if I switch back to "NAT" and log out and log in again, I have
      internet again.
    - Turns out I just need a second network adapter. In settings for
      the VM, go to "Network". Adapter 1 is "NAT"; adapter 2 is
      "Bridged network" with the name "wlp110s0". Log out and log in
      again on the Mac VM and I have both internet connection and the
      ability to ssh into the VM from my ubuntu host

---

## Updating the OS

Have difficulty updating the OS using the App Store. It downloads and
reboots but doesn't do the install properly. It seems that with
VirtualBox it's not finding the right boot file to initiate the
update.

Follow the instructions at
<https://forums.virtualbox.org/viewtopic.php?f=22&t=85631>

- Do the download and restart

- Repeatedly press <F12> to get into boot manager

- Choose "Boot Maintenance Manager"

- Choose "Boot from File"

- Select the option that has `HD(2,G`

- Choose `macOS Install Data` then `Locked Files` then `Boot Files`
  and finally `boot.efi`
