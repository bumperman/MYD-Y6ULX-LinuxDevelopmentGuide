# 3.2 Linux Kernel

Enter Kernel directory, extract it:

    cd $DEV_ROOT/Kernel
    tar -xvjf linux-4.1.tar.bz2
    cd linux-4.1

Compiling：

```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- mys_imx6_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage dtbs modules
```

When the compilation is done, the kernel image file zImage is generated in the 'arch/arm/boot' directory, and the DTB file is generated in the 'arch/arm/boot/dts' directory.

DTB File | Description
------- | ----
mys-imx6ul-14x14-evk-emmc.dtb | MYS-6ULX-IND eMMC
mys-imx6ul-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IND NAND
mys-imx6ull-14x14-evk-emmc.dtb | MYS-6ULX-IoT eMMC
mys-imx6ull-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IoT NAND

The MYS-6ULX Micro SD slot is connected to mmc0 controller.So, all dtb file is enabled with mmc0 controller.
