# 3.2 Linux Kernel

Enter Kernel directory, extract it:

```
cd $DEV_ROOT/04-Source
tar -xvf MYiR-iMX-Linux.tar.gz
cd MYiR-iMX-Linux
```

Compiling：

```
make distclean 
make myd_y6ulx_defconfig
make zImage dtbs
```

When the compilation is done, the kernel image file zImage is generated in the 'arch/arm/boot' directory, and the DTB file is generated in the 'arch/arm/boot/dts' directory.

DTB File | Description
------- | ----
myd-y6ull-14x14-gpmi-weim.dtb | MYD-Y6ULL NAND boot
myd-y6ull-14x14-emmc.dtb | MYD-Y6ULL eMMC boot
myd-y6ul-14x14-gpmi-weim.dtb | MYD-Y6UL NAND boot
myd-y6ul-14x14-emmc.dtb | MYD-Y6UL eMMC boot

The MYD-Y6ULX Micro SD slot is connected to mmc0 controller.So, all dtb files is enabled the mmc0 controller by default.

About SD card boot mode, the U-Boot default find the myd-y6ull-14x14-evk-gpmi-weim.dtb file.

When you build kernel complete, the version tag will changed automatically.If you driver load with module type, you should recompile driver module.

```
make modules
```
After compile completation, it will be installed specify path:
```
mkdir ../target-kernel
make INSTALL_MOD_PATH=../target-kernel modules_install
```
Then you can package the target-kernel directory and extract it into /lib directory on file system of MYD-Y6ULX board.
