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
mys-imx6ul-14x14-evk-emmc.dtb | MYS-6ULX-IND eMMC
mys-imx6ul-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IND NAND
mys-imx6ul-14x14-evk-emmc-myb6ulx.dtb | MYS-6ULX-IND eMMC 上安装MYB-6ULX扩展板
mys-imx6ul-14x14-evk-gpmi-weim-myb6ulx.dtb | MYS-6ULX-IND NAND 上安装MYB-6ULX扩展板
mys-imx6ull-14x14-evk-emmc.dtb | MYS-6ULX-IoT eMMC
mys-imx6ull-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IoT NAND
mys-imx6ull-14x14-evk-emmc-myb6ulx.dtb | MYS-6ULX-IoT eMMC 上安装MYB-6ULX扩展板
mys-imx6ull-14x14-evk-gpmi-weim-myb6ulx.dtb | MYS-6ULX-IoT NAND 上安装MYB-6ULX扩展板

MYS-6ULX板上的Micro SD卡槽是连接mmc0控制器，所有的dtb文件都是开启mmc0设备。

添加有"myb6ulx"标识的dtb文件，是用于支持MYB-6ULX扩展板，已配置好MYB-6ULX上的CAN，RS485，Ethernet，Camera和Audio功能，使用"myb6ulx"标识的dtb文件可以直接启动并使用相关功能。使用前请先安装好MYB-6ULX扩展板至MYS-6ULX-IOT或MYS-6ULX-IND开发板上。
