# 3.1 编译U-Boot

进入Bootloader目录，解压U-boot源码：

```
cd $DEV_ROOT/04-Source/
tar -xvf MYiR-iMX-uboot.tar.gz
cd MYiR-iMX-uboot
```

开始编译：

```
make distclean 
make <config>
make
```

这里的<config>是配置选项名称，不同的启动模式需使用不同的配置选项，MYD-Y6ULX开发板有两种选项：

启动模式 | 编译选项
-------- | --------
MYD-Y6ULX NAND Flash | myd_y6ull_14x14_nand_defconfig
MYD-Y6ULX SD Card | myd_y6ull_14x14_sd_defconfig

u-boot SD卡方式启动时默认会先检测"boot.scr"文件，这是u-boot上的脚本镜像文件，用于临时改变启动设备顺序。以下是从TFTP下载zImage和dtb文件并启动的脚本例子。使用mkimage工具"myd-y6ull-boot-mmc0-tftp.txt"文件制做成"boot.scr"文件，mkimage工具是在u-boot的tools目录下，u-boot编译完成后，mkimage也会被编译出来，直接使用即可。

```
cat myd-y6ull-boot-mmc0-tftp.txt
setenv mmcroot '/dev/mmcblk0p2 rootwait rw rootdelay=5 mem=256M'
run mmcargs
tftpboot 0x83000000 zImage
tftpboot 0x84000000 myd-y6ull-gpmi-weim.dtb
bootz 0x83000000 - 0x84000000

./tool/mkimage -A arm -T script -O linux -d myd-y6ull-boot-mmc0-tftp.txt boot.scr
```
