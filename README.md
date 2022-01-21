# Linux on Google Pixel 3a (Bonito &amp; Sargo) 
Instructions on how to install Droidian, Manjaro ARM and UBPorts on Google Pixel 3a and 3a XL (Bonito & Sargo)

##Android 9
For all 3 systems, Android 9 is required. 
BEWARE: Installing and downgrading to Android 9 will wipe your entire phone.

##Download
TWRP (latest .img) - https://dl.twrp.me/sargo/
Android 9 (choose the latest 9.0 link) - https://developers.google.com/android/images

##Flash Android 9
1. Enable OEM unlock in the Developer options under device Settings, if present.
2. Connect the device to your PC via USB.
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:
```adb reboot bootloader```
  You can also boot into fastboot mode via a key combination:
  With the device powered off, hold Volume Down + Power.
4. Once the device is in fastboot mode, verify your PC finds it by typing:
```fastboot devices```
5. Now type the following command to unlock the bootloader:
```fastboot flashing unlock```
  If the device doesn’t automatically reboot, reboot it. It should now be unlocked.
