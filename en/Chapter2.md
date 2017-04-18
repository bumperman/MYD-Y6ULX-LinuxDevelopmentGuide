# 2 Deploy Development Environment

You need to install the Linux Operation System on your host PC.Recommend to use the Ubuntu 16.04 64bit distribution, and connect the network.Next steps we will install some packages from internet.

## Connect development board with PC

1. PC use USB to RS232 cable with DEBUG port(J12) on base board.
2. Plug the power adapter into J3 interface.
3. Turn switch(J2) to DC side.

PC serial port configure parameters:

* Baudrate: 115200
* Data bit: 8bit
* Checksum: None
* Stop bit: 1bit
* Flow control: Disable

![](image/2-1.png)
Figure2-1 connection steps

## Install Necessary Software Packages

```
sudo apt-get install build-essential git-core libncurses5-dev
sudo apt-get install flex bison texinfo zip unzip zlib1g-dev gettext
sudo apt-get install u-boot-tools
sudo apt-get install g++ xz-utils
```

## Build work directory
Create a working directory to facilitate the creation of an unified environment variable path. Copy the product CD-ROM source code to the working directory, while setting the DEV_ROOT variable to convenience the follow-up step path accessed.

```
mkdir -p ~/MYD-JA5D2X-devel
export DEV_ROOT=~/MYD-JA5D2X-devel
cp -r <DVDROM>/04-Source/* $DEV_ROOT
```  

## Configure toolchain
- Cross toolchain version: gcc version 4.9.3 20141031 (prerelease) (Linaro GCC 2014.11)

```
cd $DEV_ROOT/Toolchain
tar -xvjf gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf.tar.xz
export PATH=$PATH:$DEV_ROOT/Toolchain/gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf/bin
export CROSS_COMPILE=arm-linux-gnueabihf-
export ARCH=arm
```
- Check the toolchain is correct use below command.You have setup correct environment on current SHELL when you get version infomation.If you want it always available, you need to modify your shell config file.

```
$ arm-linux-gnueabihf-gcc -v
Using built-in specs.
COLLECT_GCC=arm-linux-gnueabihf-gcc
COLLECT_LTO_WRAPPER=/home/kevinchen/SAMA5D4/gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf/bin/../libexec/gcc/arm-linux-gnueabihf/4.9.3/lto-wrapper
Target: arm-linux-gnueabihf
Configured with: /home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/snapshots/gcc-linaro-4.9-2014.11/configure SHELL=/bin/bash --with-bugurl=https://bugs.linaro.org --with-mpc=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/builds/destdir/x86_64-unknown-linux-gnu --with-mpfr=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/builds/destdir/x86_64-unknown-linux-gnu
--with-gmp=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/builds/destdir/x86_64-unknown-linux-gnu --with-gnu-as --with-gnu-ld --disable-libstdcxx-pch --disable-libmudflap --with-cloog=no --with-ppl=no --with-isl=no --disable-nls --enable-multiarch --disable-multilib --enable-c99 --with-tune=cortex-a9 --with-arch=armv7-a --with-fpu=vfpv3-d16 --with-float=hard --with-mode=thumb --disable-shared --enable-static
--with-build-sysroot=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/sysroots/arm-linux-gnueabihf --enable-lto --enable-linker-build-id --enable-long-long --enable-shared --with-sysroot=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/builds/destdir/x86_64-unknown-linux-gnu/libc --enable-languages=c,c++,fortran,lto -enable-fix-cortex-a53-835769 --enable-checking=release --with-bugurl=https://bugs.linaro.org
--with-pkgversion='Linaro GCC 2014.11' --build=x86_64-unknown-linux-gnu --host=x86_64-unknown-linux-gnu --target=arm-linux-gnueabihf --prefix=/home/buildslave/workspace/BinaryRelease/label/x86_64/target/arm-linux-gnueabihf/_build/builds/destdir/x86_64-unknown-linux-gnu
Thread model: posix
gcc version 4.9.3 20141031 (prerelease) (Linaro GCC 2014.11)
```

