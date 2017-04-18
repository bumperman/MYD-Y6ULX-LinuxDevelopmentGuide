# 3.1.1 Compiling AT91Bootstrap

MYD-JA5D2x uses AT91Bootstrap as first level bootloader. The chip power on, will start from the AT91Bootstrap program, and then boot u-boot procedures, untils the kernel started.Enter the Bootloader directory, extract at91bootstrap source tar ball:

    cd $DEV_ROOT/Bootloader
    tar -xvjf at91bootstrap.tar.bz2
    cd at91bootstraps
    
Compiling：
 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- <config>
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-

The <config> option value is different boot mode. The MYD-JA5D2 supports three boot modes.

Boot Mode | Config file
-------- | --------
NAND Flash | myd_ja5d2xnd_uboot_defconfig
SPI Flash | myd_ja5d2xdf_uboot_defconfig
