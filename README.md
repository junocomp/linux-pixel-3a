# Linux on Google Pixel 3a (Bonito &amp; Sargo) 
Instructions on how to install Droidian, Manjaro ARM and UBPorts on Google Pixel 3a and 3a XL (Bonito & Sargo)

## Android 9
<p>For all 3 systems, Android 9 is required. 
   <br><b>BEWARE:</b> Installing and downgrading to Android 9 will wipe your entire phone.</p>

## Download
<p>TWRP (latest .img - rename it twrp.img) - https://dl.twrp.me/sargo/
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

It is recommended to expand the rootfs size from <b>8GB to 48GB</b> inside <b>droidian-rootfs-api28gsi-arm64.zip.</b> Double click on the zip and enter inside the file <b>setup.sh.</b> Replace <b>8GB to 48GB.</b> Save and close the file. Then press <b>Update.</b> Make sure to do this everytime you download the latest droidian-rootfs-api28gsi-arm64.zip.

<b>ATTENTION: If you are using Ubuntu 20.04 you will need the latest fastboot, otherwise you won't be able to flash Droidian. </b>
1. Download SDK Platform Tools for Linux from https://developer.android.com/studio/releases/platform-tools
2. Place your Droidian and TWRP files inside the downloaded folder. 
3. ```./``` infront of fastboot will be require

### Flashing Droidian</b>
1. ```fastboot -aa```
2. ```fastboot reboot bootloader```
3. ```fastboot format:ext4 userdata```
4. ```fastboot boot twrp.img```
5. Wait until it TWRP boots
6. ```adb push droidian-* /tmp```
7. On TWRP head to ```Install - SD CARD (Up a Level) - tmp```
8. Flash the files in this order: ```droidian-rootfs``` ```droidian-devtools``` ```droidian-adaptation```
9. When is done reboot ```slot A```
10. The phone will restart 2 or 3 times. 
11. Password: ```1234```
12. Open Software and upgrade system.
   
### SSH
It is recommended to setup SSH right after connecting to WIFI. Make sure your phone is connected with a USB cable.

```ssh droidian@10.15.19.82```

### Upgrading to Bookworm
As of now there are no images for Bookworm (coming soon). Is recommended to upgrade from Bullseye.

1. Ensure your system is up-to-date (you can use the Software app)
2. Install the ```droidian-upgrade-bookworm``` package:

```sudo apt install droidian-upgrade-bookworm```

3. Fetch the new repositories:

```sudo apt update```
<br>```sudo apt upgrade```

4. Finally, do a standard dist-upgrade (note: it would be best doing this on-device):

```sudo apt update```
<br>```sudo apt dist-upgrade```

5. Clean up and reboot

```sudo apt clean```
<br>```sudo reboot -f```

6. Once the system reboots, open the Software app, go to the Updates tab -> Search for updates again -> Install the remaining updates

### Known Issues
1. Camera & Flashlight do not work
2. Battery life is short (better on Pixel 3a XL)
3. Waydroid installs but is very slow.
4. Finger reader does not work (on all Droidian devices)
5. Some KDE flatpak apps won't launch

### Add Staging Repo (Optional)

Change release to <b>bullseye</b> or <b>bookworm</b> depending on your release version. Add:

```deb http://staging.repo.droidian.org/ release main```

to ```/etc/apt/source.list```

### Join Droidian on Telegram
https://t.me/droidianlinux

## Manjaro ARM
Manjaro ARM is a bit slower than Droidian and it has the same known issues.

### Install
1. Download ```Manjaro-ARM-phosh-halium-9.zip``` or ```Manjaro-ARM-nemomobile-halium-9.zip``` from https://github.com/manjaro-libhybris/image-ci/releases
2. Download the Sargo files for Manjaro ARM from https://github.com/giovannicaligaris/linux-pixel-3a/releases/tag/v1
3. Add your ```twrp.img``` inside the downloaded folder
4. Run ```./flash-all.sh```
5. Head to ```Advanced``` and sideload Manjaro-ARM-*.zip
6. ```adb sideload Manjaro-ARM-**-halium-9-**.zip```
7. Sideload might get stuck at 47%, just wait patiently
8. Reboot the phone after sideloading
9. Password: ```123456```

### Adjust Resolution
Make sure your phone is connected to a USB cable.

```ssh manjaro@10.15.19.82```
<br>```sudo nano /usr/share/phosh/phoc.ini```

Add 

```[output:HWCOMPOSER-1]```
<br>```scale = 3```

Save, exit and reboot

```sudo reboot -f```

### Updating
For some reason Manjaro does not seem to remember repo keys and it won't allow to update or install packages. Install the following:

```sudo pacman-key --init && sudo pacman-key --populate```
<br>```sudo pacman -S gnupg archlinuxarm-keyring yay libpamac-flatpak-plugin iio-sensor-proxy iio-utils libhandy```

If keeps asking for GNUPG keys, just repopulate and try to install the packages that you need

```sudo pacman-key --init && sudo pacman-key --populate```

### Join Manjaro-ARM on Telegram
https://t.me/manjaroonhalium

## UBPorts
UBPorts has the most amount of support for Sargo & Bonito

https://devices.ubuntu-touch.io/device/sargo/

### Install
Check the UBPorts page on how to use their installer

https://devices.ubuntu-touch.io/installer/?pk_vid=7745a6d54b073d6c1642764968dafd25

### Join UBPorts on Telegram
https://t.me/ubports

##

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fgiovannicaligaris%2Flinux-pixel-3a&count_bg=%23A56DE2&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Views&edge_flat=false)](https://hits.seeyoufarm.com)

