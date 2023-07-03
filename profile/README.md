
SailfishOS on Asus Zenfone 8.
===

Install Instructions
===
**Fastboot commands here need to be issued from Bootloader, which is available by pressing Volume Up while powering on the phone.**

1. First, Android 11 needs to be installed. This is available now on https://www.asus.com/content/android-12-beta/ if you scroll down, there's this link to [WW-ZS590KS-30.11.51.115-MR0-user_20210826-release.zip](https://dlcdnets.asus.com/pub/ASUS/ZenFone/ZS590KS/WW-ZS590KS-30.11.51.115-MR0-user_20210826-release.zip)

1. Next Lineage 18.1 needs to be installed. I have pre-build zip here https://1drv.ms/f/s!Alh0arVfv0RwiuActTaUw-9zCecxgw?e=WFf1UG 
You need to `fastboot boot` (not install!) TWRP  https://eu.dl.twrp.me/I006D/ to install it.
You can boot Lineage to see how/if it works. 

1. To install SailfishOS you need to boot TWRP again and:
- format the data partition
- install the zip file from releases TODO instructions with TWRP touchscreen
- TBD if empty vbmeta is needed

Alternate installation instructions
--
If booting twrp does not work.
Step 1. is as above.

You may need to use `fastboot flash boot` for Lineage boot.img and `fastboot flash vendor_boot` for lineage vendor_boot.img

The Lineage recovery can be accessed by either entering Bootloader (see above) and selecting "Recovery mode" or by pressing Volume-Down while the phone is powering on.

After this, you can use "Apply Update" to install Lineage, followed by `adb sideload ` + lineage zip.

After checking lineage works ok, restart into Lineage Recovery, format the data partition and "Enable ADB".
Through `adb shll` these are the manual instructions to install (make sure `mount /data` first if not already mounted).

Unzip the Sailfish release zip.
From the host push the tar.gz file to /data
```
adb push sailfishos-sake-release-4.5.0.19-alpha2.tar.gz /data/
```

Now in `adb shell`:
```
mkdir -p /data/.stowaways/sailfishos
tar --numeric-owner -xvzf sailfishos-sake-release-4.5.0.19-alpha2.tar.gz -C /data/.stowaways/sailfishos
```

Finally, you need to get back to bootloader and `fastboot flash hybris_boot.img` (from the same Sailfish release file).

Build Instructions
===
To build LineageOS-18.1 follow https://wiki.lineageos.org/devices/sake/build

A pre-built zip is available here https://1drv.ms/f/s!Alh0arVfv0RwiuActTaUw-9zCecxgw?e=WFf1UG

To build the Sailfish image you need to follow steps from HADK but using repos in this org or mine (including patches and boot repos).

The HABUILD_SDK command are: 
```
. build/envsetup.sh
breakfast sake
make -j$(nproc --all) hybris-hal droidmedia libui_compat_layer libsfplugin_ccodec
```
(that is, it needs `libui_compat_layer` for the GUI to work, and one of the hybris-patches here acts on ccodec to make video recording work)

For community encription you need to build also `hwcrypt` (TODO build fix for A11).

Manifests
===
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project path="device/asus/sake" name="sailfishos-on-sake/android_device_asus_sake" revision="hybris-18.1" />
    <project path="kernel/asus/sm8350" name="sailfishos-on-sake/android_kernel_asus_sm8350" revision="hybris-18.1" />
    <project path="vendor/asus" name="sailfishos-on-sake/proprietary_vendor_asus" revision="lineage-18.1" />
</manifest>
````
