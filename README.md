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

# Original code: https://github.com/cfig/Android_boot_image_editor
