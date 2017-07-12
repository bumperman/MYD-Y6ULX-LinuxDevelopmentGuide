# 4 Linux应用开发

本章主要介绍MYS-6ULX开发板底板外围硬件设备应用例程的使用。

使用前，需要先安装Yocto提供的SDK工具链，再编译所有例程代码，并拷贝至开发板目录下。

## 编译应用例程

加载工具链到当前终端后，可以查看gcc的版本信息，确认当前环境已正确加载。
```
. /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-\
poky-linux-gnueabi
arm-poky-linux-gnueabi-gcc -v
Using built-in specs.
COLLECT_GCC=arm-poky-linux-gnueabi-gcc
COLLECT_LTO_WRAPPER=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/
x86_64-pokysdk-linux/usr/libexec/arm-poky-linux-gnueabi/gcc/arm-
poky-linux-gnueabi/5.3.0/lto-wrapper
Target: arm-poky-linux-gnueabi
Configured with: ../../../../../../work-shared/gcc-5.3.0-r0/gcc-
5.3.0/configure --build=x86_64-linux --host=x86_64-pokysdk-linux
--target=arm-poky-linux-gnueabi --prefix=/opt/myir-imx6ulx-fb/4.1
.15-2.0.1/sysroots/x86_64-pokysdk-linux/usr --exec_prefix=/opt/my
ir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/usr --bi
ndir=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-li
nux/usr/bin/arm-poky-linux-gnueabi --sbindir=/opt/myir-imx6ulx-fb
/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/usr/bin/arm-poky-linu
x-gnueabi --libexecdir=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots
/x86_64-pokysdk-linux/usr/libexec/arm-poky-linux-gnueabi --datadi
r=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux
/usr/share --sysconfdir=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroot
s/x86_64-pokysdk-linux/etc --sharedstatedir=/opt/myir-imx6ulx-fb/
4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/com --localstatedir=/o
pt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/var
--libdir=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysd
k-linux/usr/lib/arm-poky-linux-gnueabi --includedir=/opt/myir-imx
6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/usr/include --
oldincludedir=/opt/myir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-p
okysdk-linux/usr/include --infodir=/opt/myir-imx6ulx-fb/4.1.15-2.
0.1/sysroots/x86_64-pokysdk-linux/usr/share/info --mandir=/opt/my
ir-imx6ulx-fb/4.1.15-2.0.1/sysroots/x86_64-pokysdk-linux/usr/shar
e/man --disable-silent-rules --disable-dependency-tracking --with
-libtool-sysroot=/home/kevinchen/mys-imx6ul/fsl-release-yocto/bui
ld/tmp/sysroots/x86_64-nativesdk-pokysdk-linux --with-gnu-ld --en
able-shared --enable-languages=c,c++ --enable-threads=posix --ena
ble-multilib --enable-c99 --enable-long-long --enable-symvers=gnu
--enable-libstdcxx-pch --program-prefix=arm-poky-linux-gnueabi- -
-without-local-prefix --enable-lto --enable-libssp --enable-libit
m --disable-bootstrap --disable-libmudflap --with-system-zlib --w
ith-linker-hash-style=gnu --enable-linker-build-id --with-ppl=no 
--with-cloog=no --enable-checking=release --enable-cheaders=c_glo
bal --without-isl --with-gxx-include-dir=/not/exist/usr/include/c
++/5.3.0 --with-build-time-tools=/home/kevinchen/mys-imx6ul/fsl-r
elease-yocto/build/tmp/sysroots/x86_64-linux/usr/arm-poky-linux-g
nueabi/bin --with-sysroot=/not/exist --with-build-sysroot=/home/b
lackrose/mys-imx6ul/fsl-release-yocto/build/tmp/sysroots/mys6ul14
x14 --enable-poison-system-directories --with-mpfr=/home/blackros
e/mys-imx6ul/fsl-release-yocto/build/tmp/sysroots/x86_64-nativesd
k-pokysdk-linux --with-mpc=/home/kevinchen/mys-imx6ul/fsl-release
-yocto/build/tmp/sysroots/x86_64-nativesdk-pokysdk-linux --enable
-nls --with-arch=armv7-a
Thread model: posix
gcc version 5.3.0 (GCC) 

cd $DEV_ROOT/04-Sources
tar xvf example.tar.bz2
cd example
make
```
