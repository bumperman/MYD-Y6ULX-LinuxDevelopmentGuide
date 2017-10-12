# 4 Linux应用开发

本章主要介绍MYD-Y6ULX开发板底板外围硬件设备应用例程的使用。

使用前，需要先安装Yocto提供的SDK工具链，再编译所有例程代码，并拷贝至开发板目录下。

## 编译应用例程

加载工具链到当前终端后，可以查看gcc的版本信息，确认当前环境已正确加载。
```
$source /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-\
poky-linux-gnueabi

$ arm-poky-linux-gnueabi-gcc --version
arm-poky-linux-gnueabi-gcc (GCC) 5.3.0
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
编译示例代码：
```
$cd $DEV_ROOT/04-Sources
$tar xvf example.tar.bz2
$cd example
$make
```
