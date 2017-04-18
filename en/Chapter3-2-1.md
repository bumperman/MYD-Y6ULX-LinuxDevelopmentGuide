# 编译Linux内核

Enter Kernel目录，解压内核源码：

    cd <WORKDIR>/Kernel
    tar -xvjf linux-4.1.tar.bz2
    cd linux-4.1

开始编译：

    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean 
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- sama5_defconfig
    make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage dtbs

编译完成后在arch/arm/boot目录会生成内核镜像文件zImage，在arch/arm/boot/dts 目录会生成DTB文件。

