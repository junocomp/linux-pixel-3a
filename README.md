# Linux on Google Pixel 3a (Bonito &amp; Sargo) 
Instructions on how to install Droidian, Manjaro ARM and UBPorts on Google Pixel 3a and 3a XL (Bonito & Sargo)

## Android 9
<p>For all 3 systems, Android 9 is required. 
   <br><b>BEWARE:</b> Installing and downgrading to Android 9 will wipe your entire phone.</p>

## Download
<p>TWRP (latest .img) - https://dl.twrp.me/sargo/
<br>Android 9 (choose the latest 9.0 link) - https://developers.google.com/android/images </p>

## Unlock OEM
1. Enable OEM unlock in the Developer options under device Settings, if present.
2. Connect the device to your PC via USB.
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:
```adb reboot bootloader```
   You can also boot into fastboot mode via a key combination: With the device powered off, hold ```Volume Down + Power```
4. Once the device is in fastboot mode, verify your PC finds it by typing:
```fastboot devices```
5. Now type the following command to unlock the bootloader: ```fastboot flashing unlock``` 
6. If the device doesn’t automatically reboot, reboot it. It should now be unlocked.

## Flash Android 9
You will need to flash Android on both A & B partitions. Open the terminal inside the download Android 9 folder.

1. Flash partition B first
2. ```fastboot -ab```
3. ```fastboot reboot bootloader```
4. ```./flash-all.sh```
5. This will take a few minutes and it will then boot into Android. There is no need to setup the phone. Just go back into the bootloader by holding hold ```Volume Down + Power```
6. Flash A partition
7. ```fastboot -aa```
8. Follow steps 2 to 5 again

## Droidian
<p>Download the following files from https://github.com/droidian-images/rootfs-api28gsi-all/releases
<br> This will install Debian Bullseye</p>

1. droidian-rootfs-api28gsi-arm64.zip
2. droidian-devtools-arm64.zip
3. droidian-adaptation-google-sargo-arm64.zip

