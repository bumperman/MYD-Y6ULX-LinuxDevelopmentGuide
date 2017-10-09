# 3 构建系统

本章主要介绍MYD-Y6ULX开发板上, Linux操作系统相关部件的编译和使用。MYD-Y6ULX的Linux系统包含以下部件:

* U-Boot: 引导程序，支持不同方式启动内核。
* Linux Kernel: 适用于MYD-Y6ULX开发板的Linux 4.1.15内核，同时包含支持板载外设的驱动。
* Yocto: 一个开源协作项目，提供丰富的模板、工具和方法来支持构建出面向嵌入式产品的自定义Linux系统。

本章中用到的代码存放在资源包04-Source目录下，部分软件包的文件名中有标识号，后文不再特别说明。

编前u-boot和Linux内核代码前，请先安装meta-toolchain并加载环境变量到当前shell。
