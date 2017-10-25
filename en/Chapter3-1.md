# 3.1 Compiling U-Boot

Enter Bootloader directory, extract U-boot source tar source package:

```
cd $DEV_ROOT/04-Source
tar -xvf MYiR-iMX-uboot.tar.gz
cd MYiR-iMX-uboot
```

Compiling：
 
```
make distclean 
make <config>
make
```

The <config> option value is different boot mode. The MYD-Y6ULX supports two boot modes.

Boot Mode | Config file
-------- | --------
MYD-Y6ULX NAND Flash | myd_y6ull_14x14_nand_defconfig
MYD-Y6ULX SD Card | myd_y6ull_14x14_sd_defconfig

U-Boot SD boot mode will search and execute a script file "boot.scr" when U-Boot booting up. It used to change boot type in temporary.Next is use TFTP to download zImage and dtb to boot system as example. Using mkimage tool through "myd-y6ull-boot-mmc0-tftp.txt" to generate the "boot.scr" file as example. The mkimage tool source code is locating in "U-Boot/tools" directory. It will be compiled after U-Boot compiled.

```
cat myd-y6ull-boot-mmc0-tftp.txt
setenv mmcroot '/dev/mmcblk0p2 rootwait rw rootdelay=5 mem=256M'
run mmcargs
tftpboot 0x83000000 zImage
tftpboot 0x84000000 myd-y6ull-gpmi-weim.dtb
bootz 0x83000000 - 0x84000000

./tool/mkimage -A arm -T script -O linux -d myd-y6ull-boot-mmc0-tftp.txt boot.scr
```
