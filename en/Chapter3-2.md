# 3.2 Linux Kernel

Enter Kernel directory, extract it:

    cd $DEV_ROOT/04-Source
    tar -xvf linux-4.1.15.tar.gz
    cd linux-4.1.15

Compiling：

```
make distclean 
make mys_imx6_defconfig
make zImage dtbs modules
```

When the compilation is done, the kernel image file zImage is generated in the 'arch/arm/boot' directory, and the DTB file is generated in the 'arch/arm/boot/dts' directory.

DTB File | Description
------- | ----
mys-imx6ul-14x14-evk-emmc.dtb | MYS-6ULX-IND eMMC
mys-imx6ul-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IND NAND
mys-imx6ull-14x14-evk-emmc.dtb | MYS-6ULX-IoT eMMC
mys-imx6ull-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IoT NAND

The MYS-6ULX Micro SD slot is connected to mmc0 controller.So, all dtb file is enabled with mmc0 controller.
