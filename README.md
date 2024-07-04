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
https://github.com/cfig/Android_boot_image_editor
