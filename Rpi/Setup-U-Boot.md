## Setup U-Boot for RPi   
[original guide](https://blog.night-shade.org.uk/2015/05/booting-a-raspberry-pi2-with-u-boot-and-hyp-enabled/)   
Using u-boot isn’t strictly needed. Mainline u-boot has support for the Raspberry Pi 2 so it’s a fairly simple process.   
Add cross tool chain (Crosstool-NG from previous work) to global variable then
```sh
export ARCH=arm
export CROSS_COMPILE=arm-unknown-linux-gnueabihf-
```

Download U-Boot and make it. 
```sh
git clone git://git.denx.de/u-boot.git
cd u-boot
make rpi_2_defconfig
make all
```
edit file config.txt in SD-Card. Comment all old config then add.
```sh
kernel=u-boot.bin
```
### After this part, You will nedd serial console on RPi.
