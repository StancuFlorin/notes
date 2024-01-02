---
title: "How to install LineageOS 19 on Huawei P10"
date: 2024-01-02
---

# Prerequisites

To flash a fresh LineageOS image on your Huawei P10 phone, you’ll need to install special tools and be able to boot your phone in certain modes.

## fastboot mode

To enter fastboot mode, first turn off your phone. Then, connect your phone to your PC using a USB cable. While holding down the volume down key on your phone, connect the phone to your PC. You should see a screen similar to the one in the photo below. Now you can use `fastboot` commands from your terminal.

![fastboot_mode](/assets/img/posts/huawei_p10/fastboot_mode.jpeg)

## Android Debug Bridge tool

To run `adb` and `fastboot` commands from your terminal, you’ll need to install them on your computer. You can find detailed instructions on how to install adb and fastboot on Windows, Linux, and MacOS on the [XDA Developers](https://www.xda-developers.com/install-adb-windows-macos-linux/) website.

## Drivers

Install [HiSuite](https://consumer.huawei.com/en/support/hisuite/) and hope that the drivers that comes with it are good enough.

# Unlocking the bootloader

- To unlock the bootloader, you’ll need to dissamble your device and short-circuit the testpoint. [PotatoNV](https://github.com/mashed-potatoes/PotatoNV) is a simple tool that can help you with this. You can find detailed instructions on how to use PotatoNV, in the documentation on GitHub. Make sure to read the "Entering download mode" section of the PotatoNV documentation carefully.

![testpoint](/assets/img/posts/huawei_p10/testpoint.jpeg)

- Once you have obtained the unlock code from PotatoNV, you can use the following command to unlock the bootloader. Please note that your device must be booted into fastboot mode in order to use this command.
```
fastboot oem unlock YOUR_CODE_HERE
```

![PotatoNV](/assets/img/posts/huawei_p10/PotatoNV.png)

## Flashing LineageOS 19

- Download the LineageOS GSI image created by [Andy Yan](https://sourceforge.net/projects/andyyan-gsi/files/). I used  `lineage-19.1-20231017-UNOFFICIAL-arm64_bvS.img.xz` because I wanted the system-as-root version, vanilla (without Google apps) built with PHH Superuser.
- Before you can use the system image, you’ll need to extract it from the .xz archive and obtain a .img file. Once you have the .img file, you can flash it in fastboot mode using the following command:

```
fastboot flash system lineage-19.1-20231017-UNOFFICIAL-arm64_bvS.img
```
After flashing the system image, you should see something similar to this.
```
Sending sparse 'system' 1/5 (441726 KB)            OKAY [ 10.478s]
Writing 'system'                                   OKAY [  5.104s]
Sending sparse 'system' 2/5 (460796 KB)            OKAY [ 10.595s]
Writing 'system'                                   OKAY [  4.493s]
Sending sparse 'system' 3/5 (460796 KB)            OKAY [ 10.695s]
Writing 'system'                                   OKAY [  4.481s]
Sending sparse 'system' 4/5 (427813 KB)            OKAY [  9.889s]
Writing 'system'                                   OKAY [  4.217s]
Sending sparse 'system' 5/5 (260481 KB)            OKAY [  6.052s]
Writing 'system'                                   OKAY [  2.993s]
Finished. Total time: 72.490s
```
- Reboot your phone using `fastboot reboot` and press and hold the volume up button for 3 seconds while the phone is in the state bellow. Once you’re in recovery mode, you’ll need to wipe data/factory reset.

![boot](/assets/img/posts/huawei_p10/boot.jpeg)

- Now you have a working phone using LineageOS 19 (Android 12).

## Fixes

Because the GSI version of LineageOS is not fully compatible with Huawei P10, you’ll need to run a custom script each time the phone starts. This is why I chosed to install the rooted version of the system image.

If you’re having trouble entering your WiFi password, you may need to apply the touchscreen fix manually. This step is optional if your WiFi password doesn’t contain letters that are on the edge of the keyboard or if you’re using mobile data to connect to the internet.

```
adb root
adb shell stop aptouch
```

### Apply the fixes automatically when your phone starts

- First, you’ll need to install [F-Droid](https://f-droid.org/en/packages/org.fdroid.fdroid/), an open-source app store. You can download the apk from its website at f-droid.org and sideload it to your phone. Once you’ve installed F-Droid, you can use it to install other open-source apps.
- Install [Superuser](https://github.com/phhusson/Superuser) from [F-Droid store](https://f-droid.org/en/packages/me.phh.superuser/). This is similar with SuperSU, but it is open-source and works out of the box with the already rooted version of LineageOS.
- Install [Init.d Light](https://github.com/x1125/initd-light) from [F-Droid store](https://f-droid.org/en/packages/x1125io.initdlight/). This will be used to run the script automatically.
- Start Init.d app and choose to always allow root access. You should see "Root access check: OK".
- From your PC terminal, create the script that will run automatically:
```
adb root
adb shell
cd /data/user/0/x1125io.initdlight/files
touch fix_gsi.sh
chmod +x fix_gsi.sh
```
- `fix_gsi.sh` should contain the following fixes:

```
# Fix for Speakers
echo "applying speakers fix"
chown root:audio /dev/nxp_smartpa_dev
chmod 0660 /dev/nxp_smartpa_dev
echo "done"

# Touchscreen Issue
echo "applying touchscreen fix"
stop aptouch
echo "done"
```

- Back to Init.d app, use "test scripts" button to see if your script runs smootly.
- Reboot your phone and check if the fixes are automatically applied.

### Resources

[1] [https://xdaforums.com/t/huawei-p10-vtr-l29-dual-sim-and-lineage-18-1-19-1-20.4579071/](https://xdaforums.com/t/huawei-p10-vtr-l29-dual-sim-and-lineage-18-1-19-1-20.4579071/) \\
[2] [https://github.com/phhusson/treble_experimentations/wiki/Huawei-P10-and-P10-Plus](https://github.com/phhusson/treble_experimentations/wiki/Huawei-P10-and-P10-Plus) \\
[3] [https://github.com/Coconutat/Huawei-GSI-And-Modify-Or-Support-KernelSU-Tutorial/wiki](https://github.com/Coconutat/Huawei-GSI-And-Modify-Or-Support-KernelSU-Tutorial/wiki) \\
[4] [https://github.com/Iceows/huawei-creator/tree/android-12](https://github.com/Iceows/huawei-creator/tree/android-12)