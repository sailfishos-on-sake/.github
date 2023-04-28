
SailfishOS on Asus Zenfone 8.
===

Install Instructions
===
First Lineage 18.1 needs to be installed. I have pre-build zip here https://1drv.ms/f/s!Alh0arVfv0RwiuActTaUw-9zCecxgw?e=WFf1UG

You need to `fastboot boot` (not install!) TWRP  https://eu.dl.twrp.me/I006D/ to install it.

You can boot Lineage to see how/if it works. 

To install SailfishOS you need to boot TWRP again and:
- format the data partition
- install the zip file from releases TODO

Build Instructions
===
To build LineageOS-18.1 follow https://wiki.lineageos.org/devices/sake/build

A pre-built zip is available here https://1drv.ms/f/s!Alh0arVfv0RwiuActTaUw-9zCecxgw?e=WFf1UG

To build the Sailfish image you need to follow steps from HADK but using repos in this org or mine (including patches and boot repos).

The HABUILD_SDK command are: 
```
. build/envsetup.sh
breakfast sake
TEMPORARY_DISABLE_PATH_RESTRICTIONS=true make -j$(nproc --all) hybris-hal droidmedia libui_compat_layer
```
(that is, it needs `libui_compat_layer`)

Manifests
===
```
<manifest>
        <remote name="b100dian" fetch="https://github.com/b100dian" revision="hybris-11.0" />
        <remote name="lineage" fetch="https://github.com/LineageOS" revision="lineage-18.1" />
        <remote name="them" fetch="https://github.com/TheMuppets" revision="lineage-18.1" />

        <project path="device/asus/sake" name="android_device_asus_sake" remote="lineage" />
        <project path="kernel/asus/sm8350" name="android_kernel_asus_sm8350" remote="b100dian" />
        <project path="vendor/asus" name="proprietary_vendor_asus" remote="them" revision="lineage-18.1" />
</manifest>
````
