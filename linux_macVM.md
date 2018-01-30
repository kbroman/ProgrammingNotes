## Creating a Mac High Sierra VM on Ubuntu

Initially following notes at
<http://suzywu2014.github.io/ubuntu/2017/02/23/macos-sierra-virtualbox-vm-on-ubuntu>

Then switched to the primary source, <https://github.com/geerlingguy/macos-virtualbox-vm>

Then switched to <http://tobiwashere.de/2017/10/virtualbox-how-to-create-a-macos-high-sierra-vm-to-run-on-a-mac-host-system/>

Then tried <https://www.howtogeek.com/289594/how-to-install-macos-sierra-in-virtualbox-on-windows-10/>

1. On Mac, download Sierra installer from
   <https://itunes.apple.com/us/app/macos-sierra/id1127487414?ls=1&mt=12>

2. Also on Mac, prepare the Sierra installer

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
   version: Mac OS X 10.12 Sierra (64-bit)
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

4. On command line:

   ```
   VBoxManage modifyvm "MacVM" --cpuidset 00000001 000306a9 04100800 7fbae3ff bfebfbff
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "MacBookPro11,3"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Mac-2BD1B31983FE1663"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
   VBoxManage setextradata "MacVM" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
   ```

5. Install High Sierra:

   - Open Settings for the MacSierraVM in VirtualBox
   - Click on Storage
   - Click on the CD drive
   - Click the disk on the far right and select "Choose Virtual
     Optical Disk File" and select the `Sierra.iso` file
   - Start the VM

6. Really terrible looking errors scroll by; hung in there and the
   thing _did_ fire up.
