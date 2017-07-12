# 3.1 编译U-Boot

进入Bootloader目录，解压U-boot源码：

    cd $DEV_ROOT/04-Source/
    tar -xvf u-boot-2016.03.tar.gz
    cd u-boot-2016.03

开始编译：

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- <config>
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-

这里的<config>是配置选项名称，不同的启动模式需使用不同的配置选项，MYS-6ULX开发板四种选项：

启动模式 | 编译选项
-------- | --------
MYS-6ULX-IND NAND Flash | mys_imx6ul_14x14_nand_defconfig
MYS-6ULX-IND eMMC Flash | mys_imx6ul_14x14_emmc_defconfig
MYS-6ULX-IoT NAND Flash | mys_imx6ull_14x14_nand_defconfig
MYS-6ULX-IoT eMMC Flash | mys_imx6ull_14x14_emmc_defconfig

u-boot启动时默认会先检测"boot.scr"文件，这个是u-boot上的脚本镜像文件，用于临时改变启动设备或从Micro SD启动时，可以使用此文件。以下是"mys-imx6ul-boot-sdcard.txt"文件生成"boot.scr"文件的例子，mkimage工具是在u-boot的tools目录下，u-boot编译完成后，mkimage也会被编译出来，直接使用即可。

```
cat mys-imx6ul-boot-sdcard.txt
setenv mmcroot '/dev/mmcblk0p2 rootwait rw rootdelay=5 mem=256M'
setenv mmcargs 'setenv bootargs console=${console},${baudrate} \
root=${mmcroot} mtdparts=gpmi-nand:5m(boot),10m(kernel),1m(dtb),\
-(rootfs)'
run mmcargs
fatload mmc 0 0x83000000 zImage
fatload mmc 0 0x84000000 mys-imx6ul-14x14-evk-emmc.dtb
bootz 0x83000000 - 0x84000000

./tool/mkimage -A arm -T script -O linux -d \
mys-imx6ul-boot-sdcard.txt boot.scr
```
