# 3.2 Linux Kernel

Enter Kernel directory, extract it:

    cd $DEV_ROOT/Kernel
    tar -xvjf linux-4.1.tar.bz2
    cd linux-4.1

Compiling：

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- sama5_defconfig
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage dtbs

When the compilation is donw, the kernel image file zImage is generated in the 'arch/arm/boot' directory, and the DTB file is generated in the 'arch/arm/boot/dts' directory.
