# 3.4 Compiling QT

Buildroot can be build Qt5 library and package to target file system. We also support config file to more convient to build Qt5 into file system.

 The config file "myd_ja5d2x_qt5_defconfig" default is download toolchain package from internet, you need put the our toolchain to "dl" directory(if not exist, please create it).

```
cd $DEV_ROOT/04-Sources
tar xvjf buildroot.tar.bz2
cd buildroot
cp <workspace>/gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf.tar.xz dl/
make myd_ja5d2x_qt5_defconfig
make -j4
```

Waiting for compile finish, Qt5 will be package file to "output/images" directory. The "output/host" directory can be used as Qt SDK to compile third application.

