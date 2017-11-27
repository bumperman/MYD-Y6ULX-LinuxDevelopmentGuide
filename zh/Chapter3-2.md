# 3.2 Linux Kernel

进入Kernel目录，解压内核源码：

```
cd $DEV_ROOT/04-Source
tar -xvf MYiR-iMX-Linux.tar.gz
cd MYiR-iMX-Linux
```

开始编译：

```
make distclean 
make myd_y6ulx_defconfig
make zImage dtbs
```

编译完成后在"arch/arm/boot"目录会生成内核镜像文件zImage，在"arch/arm/boot/dts"目录会生成DTB文件。

DTB文件 | 备注
------- | ----
myd-y6ull-gpmi-weim.dtb | MYD-Y6ULX NAND启动方式

MYD-Y6ULX板上的Micro SD卡槽是连接mmc0控制器，所有的dtb文件都是默认启用mmc0控制器。

SD卡方式启动时，U-Boot默认查找的文件是myd-imx6ull-14x14-evk-gpmi-weim.dtb文件。

更新kernel后，由于版本标识改变，若驱劝是以模块方式加载，需要重新编译驱动模块:

```
make modules
```
编译后，可以安装在指定位置：
```
mkdir ../target-kernel
make INSTALL_MOD_PATH=../target-kernel modules_install
```
这样就可以把target-kernel目录打包后，解压在MYD-Y6ULX开发板的/lib目录下使用。
