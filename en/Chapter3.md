# 3 Build Linux System

This chapter introduces how to build componments of Linux system. The MYD-Y6ULX includes below parts:

* U-Boot: First level bootloader.
* Linux Kernel: Linux kernel 4.1.15 and drivers suit for MYD-Y6ULX board.
* Yocto: an open source collaboration project that provides templates, tools and methods to help you create custom Linux-based system for embedded products regardless of the hardware architecture.

These software are locate in 04-Source directory.Some packages use ID number in file name.

Before compile u-boot and Linux kernel source code, you need install meta-toolchain and load the environment variables into current shell.
