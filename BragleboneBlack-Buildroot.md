ARM (little endian)

select cortex-A8 as the Target Architecture Variant.

EABIhf

ELF is the only available Target Binary Format

Select External toolchain, Select Linaro 2016.02 as the Toolchain

enable the Linux kernel option

Select Custom version as the Kernel version, and enter 4.6 in the Kernel

http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/arm/configs/?id=v4.6

omap2plus in the Defconfig name option

zImage format

http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/arm/boot/dts/?id=v4.6

a device tree present in the kernel, and type am335x-boneblack as the Device Tree Source file names

enabling Busybox

Filesystem images menu. For now, keep only the tar the root filesystem option

ARM bootloader, U-Boot

Kconfig

2016.03 version as the U-Boot version

http://git.denx.de/?p=u-boot.git;a=tree;f=configs

am335x_boneblack in Board defconfig

U-Boot on AM335x is split in two parts: the first stage bootloader called MLO and the second stage bootloader called u-boot.img. So, select u-boot.img as the U-
Boot binary format, enable Install U-Boot SPL binary image and use MLO as the U-Boot SPL binary image name.

### MLO is not in /output/image, it locates in /output/build/uboot-2016.03/ 
