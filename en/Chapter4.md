# 4 Linux Application Development

The hardware peripherals and application examples of MYD-Y6ULX development board.

Before use, you need use Yocto SDK toolchain to compile all the example code, and copy to the development board directory.


## Compile example program

Load the toolchain environment to current shell, and check the gcc version to verify environment correct.

```
$source /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-\
cortexa7hf-neon-poky-linux-gnueabi

$arm-poky-linux-gnueabi-gcc --version
$arm-poky-linux-gnueabi-gcc --version
arm-poky-linux-gnueabi-gcc (GCC) 5.3.0
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.


```

```
$cd $DEV_ROOT/04-Sources
$tar xvf example.tar.bz2
$cd example
$make
```
