# 3.2 Linux Kernel

进入Kernel目录，解压内核源码：

    cd $DEV_ROOT/Kernel
    tar -xvjf linux-4.1.tar.bz2
    cd linux-4.1

开始编译：

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- mys_imx6_defconfig
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage dtbs modules

编译完成后在"arch/arm/boot"目录会生成内核镜像文件zImage，在"arch/arm/boot/dts"目录会生成DTB文件。

DTB文件 | 备注
------- | ----
mys-imx6ul-14x14-evk-emmc.dtb | MYS-6UL eMMC
mys-imx6ul-14x14-evk-gpmi-weim.dtb | MYS-6UL NAND
mys-imx6ull-14x14-evk-emmc.dtb | MYS-6ULL eMMC
mys-imx6ull-14x14-evk-gpmi-weim.dtb | MYS-6ULL NAND

MYS6ULx板上的Micro SD卡槽是连接mmc0控制器，所有的dtb文件都是开启mmc0设备。当板载的存储器是NAND或eMMC时，需要从Micro SD卡启动，可以使用同类的dtb文件。
