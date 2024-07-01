<<<<<<< HEAD
<<<<<<< HEAD
## Installation
```
sudo apt install git device-tree-compiler lz4 xz-utils zlib1g-dev openjdk-17-jdk gcc g++ python3 python-is-python3 p7zip-full android-sdk-libsparse-utils && cd $home && git clone https://github.com/loli067/bedit && cd bedit && sh setup.sh
``` 
## Usage 
```
bedit --help
``` 
## Note 
```
Remember to type in .img
```
```
The unpacked boot image will be saved in a directory called unpacked_boot_image.
```
```
DO NOT run bedit with sudo e.g
sudo bedit unpack <filename>
sudo bedit pack
```
## Credits
I only made a script for the android_boot_image_editor to make it simplere to use All credits for the original code goto
##
Cfig , CallMESuper , Surendrajat , hamjin , sapphire-hk , rover12421 , scarlet-glass , codacy-badger , 918712886438 , 10S-trace , jonas-app
##
Original code: https://github.com/cfig/Android_boot_image_editor
=======
# Android_boot_image_editor
[![CI](https://github.com/cfig/Android_boot_image_editor/actions/workflows/main.yml/badge.svg)](https://github.com/cfig/Android_boot_image_editor/actions/workflows/main.yml)
[![License](http://img.shields.io/:license-apache-blue.svg?style=flat-square)](http://www.apache.org/licenses/LICENSE-2.0.html)

A tool for reverse engineering Android ROM images.

##  Requirements
Make sure you have [JDK11+](https://www.oracle.com/java/technologies/downloads/#java17) and [Python3](https://www.python.org/downloads/).

* Linux / WSL: `sudo apt install git device-tree-compiler lz4 xz-utils zlib1g-dev openjdk-17-jdk gcc g++ python3 python-is-python3 p7zip-full android-sdk-libsparse-utils erofs-utils`

* Mac: `brew install lz4 xz dtc`

* Windows: Install openssl and device-tree compiler with [chocolate](https://chocolatey.org/install)
`choco install openssl dtc-msys2`

## Getting Started
Put your boot.img to current directory, then start gradle 'unpack' task:

```bash
cp <original_boot_image> boot.img
./gradlew unpack
=======
## Installation
>>>>>>> 5dc2710 (Update 14_r3)
```
sudo apt install git device-tree-compiler lz4 xz-utils zlib1g-dev openjdk-17-jdk gcc g++ python3 python-is-python3 p7zip-full android-sdk-libsparse-utils && cd $home && git clone https://github.com/loli067/bedit && cd bedit && sh setup.sh
``` 
## Usage 
```
bedit --help
``` 
## Note 
```
Remember to type in .img
```
```
The unpacked boot image will be saved in a directory called unpacked_boot_image.
```
```
DO NOT run bedit with sudo e.g
sudo bedit unpack <filename>
sudo bedit pack
```
<<<<<<< HEAD

</details>

<details>

  <summary>How to pull device tree blob(dtb) from a rooted device</summary>

If you have a rooted device and want to pull /proc/device-tree
```bash
touch fake.dtb
./gradlew pull
```
This tool will copy `dtc` to the target device via `adb`, and dump the dtb and dts file. Eventually you should get something like this
```
+--------+------------------------------+
|  What  |            Where             |
+--------+------------------------------+
| source | /proc/device-tree            |
+--------+------------------------------+
| DTB    | panther.dtb                  |
+--------+------------------------------+
| DTS    | build/unzip_boot/panther.dts |
+--------+------------------------------+

```

</details>

<details>

  <summary>How to work edit device tree blob(dtb) file</summary>

If you have a dtb file and want to edit its content
```bash
cp <your_dtb_file> .
./gradlew unpack
```
This tool will decompile it and put the decompiled source to build/unzip_boot.

```
                        Unpack Summary of panther.dtb
+------+------------------------------+
| What |            Where             |
+------+------------------------------+
| DTB  | panther.dtb                  |
+------+------------------------------+
| DTS  | build/unzip_boot/panther.dts |
+------+------------------------------+
```

</details>

<details>
  <summary>working with system.img</summary>

```bash
cp <your_system_image> system.img
./gradlew unpack
```
You get `system.img.unsparse`, that's a plain ext4 filesystem data.

</details>

<details>
  <summary>How to disable AVB verification</summary>

The idea is to set flag=2 in main vbmeta.

```bash
rm *.img
cp <your_vbmeta_image> vbmeta.img
./gradlew unpack
vim -u NONE -N build/unzip_boot/vbmeta.avb.json  -c ":19s/0/2/g" -c ":wq"
./gradlew pack
```
Then flash vbmeta.img.signed to your device.

</details>

<details>

  <summary>How to merge init_boot.img into boot.img</summary>

* unpack init_boot.img and copy out "build/unzip_boot/root".
* clear workspace by `gradle clear`, then unpack boot.img
* copy back the "build/unzip_boot/root"
* edit build/unzip_boot/boot.json
- change `ramdisk.size` to 1
- change `ramdisk.file` from "build/unzip_boot/ramdisk.img" to "build/unzip_boot/ramdisk.img.lz4"

</details>

<details>

  <summary>work with payload.bin</summary>

- extract everything

Usage:
```
    gradle unpack
```

- extract only 1 specified partition
Usage:
```
    gradle unpack -Dpart=<part_name>
```
Example:
```
    gradle unpack -Dpart=boot
    gradle unpack -Dpart=system
```

Note:
    "build/payload/" will be deleted before each "unpack" task

</details>


<details>

  <summary>work with apex images</summary>

AOSP already has tools like apexer, deapexer, sign_apex.py, these should suffice the needs on .apex and .capex.
Refer to Issue https://github.com/cfig/Android_boot_image_editor/issues/120

- For those who may be interested in apex generation flow, there is a graph here
![image](doc/apexer_generate_flow.png)

</details>

<details>
  <summary>How to work with vendor_dlkm.img</summary>

```bash
cp <your_vendor_dlkm.img> vendor_dlkm.img
cp <your_vbmeta_image> vbmeta.img
./gradlew unpack
# replace your .ko
./gradlew pack
```
Then flash `vbmeta.img.signed` and `vendor_dlkm.img.signed` to the device.

</details>

## boot.img layout
Read [boot layout](doc/layout.md) of Android boot.img and vendor\_boot.img.
Read [misc layout](doc/misc_image_layout.md) of misc\.img

## References and Acknowledgement
<details>
  <summary>more ...</summary>

Android version list https://source.android.com/source/build-numbers.html<br/>
Android build-numbers https://source.android.com/setup/start/build-numbers

cpio & fs\_config<br>
https://android.googlesource.com/platform/system/core<br/>
https://www.kernel.org/doc/Documentation/early-userspace/buffer-format.txt<br/>
AVB<br/>
https://android.googlesource.com/platform/external/avb/<br/>
boot\_signer<br/>
https://android.googlesource.com/platform/system/extras<br/>
mkbootimg<br/>
https://android.googlesource.com/platform/system/tools/mkbootimg/+/refs/heads/master/<br/>
boot header definition<br/>
https://android.googlesource.com/platform/system/tools/mkbootimg/+/refs/heads/master/include/bootimg/bootimg.h<br/>
kernel info extractor<br/>
https://android.googlesource.com/platform/build/+/refs/heads/master/tools/extract_kernel.py<br/>
mkdtboimg<br/>
https://android.googlesource.com/platform/system/libufdt/<br/>
libsparse<br/>
https://android.googlesource.com/platform/system/core/+/refs/heads/master/libsparse/<br/>
Android Nexus/Pixle factory images<br/>
https://developers.google.cn/android/images<br/>

</details>

This project is developed with products by Jetbrains.

<a href="https://jb.gg/OpenSource">
  <img src="https://user-images.githubusercontent.com/1133314/116802621-c076be80-ab46-11eb-8a14-9454a933de7d.png" alt="drawing" width="80">
</a>
>>>>>>> 5a28c8c (Updated to 14_3)
=======
## Credits
I only made a script for the android_boot_image_editor to make it simplere to use All credits for the original code goto
##
Cfig , CallMESuper , Surendrajat , hamjin , sapphire-hk , rover12421 , scarlet-glass , codacy-badger , 918712886438 , 10S-trace , jonas-app
##
Original code: https://github.com/cfig/Android_boot_image_editor
>>>>>>> 5dc2710 (Update 14_r3)
