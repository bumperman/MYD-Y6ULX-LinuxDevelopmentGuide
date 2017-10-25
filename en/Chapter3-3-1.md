# 3.3.1 Yocto build Linux system

This section suit for developer on customization file system.If you just want to use it, please use the prebuilt file system.

The Yocto needs download all third-party software packages from internet.In order to build more speedly, MYD-Y6ULX also support a full package, you desn't need download again.

Attention: Building Yocto does not use previous toolchain, please open new tab for shell or new terminal window.

## MYD-Y6ULX support full Yocto package

Extract Yocto source package, and extract the Yocto-downloads.tar.xz into Yocto source direcotry.The Yocto-downloads.tar.xz includes all packages when building MYD-Y6ULX from Yocto.

Attention: The Yocto-downloads.tar.xz file is more large, it is not include in MYD-Y6ULX iso file.Please visit and download it from http://d.myirtech.com/MYD-Y6ULX.

```
cd $DEV_ROOT
tar xvf 04-Source/fsl-release-yocto.tar.xz
tar xvf 04-Source/Yocto-downloads.tar.xz -C fsl-release-bsp
cd fsl-release-bsp
```

Last, also needs put the kernel and u-boot source into your home directory in linux.It will be fetched with Yocto.

```
cd $DEV_ROOT
tar xvf 04-Source/MYiR-iMX-Linux.tar.gz -C ~/
tar xvf 04-Source/MYiR-iMX-uboot.tar.bz -C ~/
```

## Init Yocto build directory
Use script by NXP supported, create a build directory, and Yocto will build all under it.
The MACHINE value is "myd-y6ull14x14".

```
DISTRO=myir-imx-fb MACHINE=myd-y6ull14x14 source fsl-setup-release.sh -b build
tree conf/
conf/
├── bblayers.conf
├── bblayers.conf.org
├── local.conf
├── local.conf.org
├── local.conf.sample
├── sanity_info
└── templateconf.cfg
```

## Build system image with Qt5 package
The first build will cost more time, please take a coffee and wait it completion.
```
bitbake fsl-image-qt5
```

## Build system image with full command line packages
You doesn't need to modify any file, just let Yocto to build it.

```
bitbake core-image-base
```

Image Name | Description | Used for
---------- | ------ | -----------------
core-image-minimal | minimal file system | used for MYD-Y6ULX to update system
core-image-base | base file system has more command line feature | full commnand line system, no GUI
fsl-image-qt5 | system use Qt5 as GUI | used for graphics requirment

After build process finish, it will output manifest file.This file has each package name and version be installed to target file system.

The first build process of Yocto will take more time, this depend on your PC cpu core number and RAM size. The Yocto recommend use eight core CPU and SSD hardware to impove build speed. Additionally, the Yocto will generate cache after first build, the next build process also save more time for you.

All output files are in "tmp/deploy/images/myd-y6ul14x14/" directory after build complete. Below as example:

```
ls -lh tmp/deploy/images/myd-y6ull14x14/
total 1.4G
-rw-r--r-- 1 kevinchen kevinchen  64M Oct 11 16:16 core-image-base-myd-y6ull14x14-20171011081338.rootfs.ext4
-rw-r--r-- 1 kevinchen kevinchen 4.4K Oct 11 16:16 core-image-base-myd-y6ull14x14-20171011081338.rootfs.manifest
-rw-r--r-- 1 kevinchen kevinchen  80M Oct 11 16:16 core-image-base-myd-y6ull14x14-20171011081338.rootfs.sdcard
-rw-r--r-- 1 kevinchen kevinchen  15M Oct 11 16:16 core-image-base-myd-y6ull14x14-20171011081338.rootfs.tar.bz2
-rw-r--r-- 1 kevinchen kevinchen  11M Oct 11 16:16 core-image-base-myd-y6ull14x14-20171011081338.rootfs.tar.xz
-rw-r--r-- 1 kevinchen kevinchen  64M Oct 11 16:48 core-image-base-myd-y6ull14x14-20171011084756.rootfs.ext4
-rw-r--r-- 1 kevinchen kevinchen 4.4K Oct 11 16:48 core-image-base-myd-y6ull14x14-20171011084756.rootfs.manifest
-rw-r--r-- 1 kevinchen kevinchen  80M Oct 11 16:48 core-image-base-myd-y6ull14x14-20171011084756.rootfs.sdcard
-rw-r--r-- 1 kevinchen kevinchen  15M Oct 11 16:48 core-image-base-myd-y6ull14x14-20171011084756.rootfs.tar.bz2
-rw-r--r-- 1 kevinchen kevinchen  11M Oct 11 16:48 core-image-base-myd-y6ull14x14-20171011084756.rootfs.tar.xz
lrwxrwxrwx 1 kevinchen kevinchen   57 Oct 11 16:48 core-image-base-myd-y6ull14x14.ext4 -> core-image-base-myd-y6ull14x14-20171011084756.rootfs.ext4
lrwxrwxrwx 1 kevinchen kevinchen   61 Oct 11 16:48 core-image-base-myd-y6ull14x14.manifest -> core-image-base-myd-y6ull14x14-20171011084756.rootfs.manifest
lrwxrwxrwx 1 kevinchen kevinchen   59 Oct 11 16:48 core-image-base-myd-y6ull14x14.sdcard -> core-image-base-myd-y6ull14x14-20171011084756.rootfs.sdcard
lrwxrwxrwx 1 kevinchen kevinchen   60 Oct 11 16:48 core-image-base-myd-y6ull14x14.tar.bz2 -> core-image-base-myd-y6ull14x14-20171011084756.rootfs.tar.bz2
lrwxrwxrwx 1 kevinchen kevinchen   59 Oct 11 16:48 core-image-base-myd-y6ull14x14.tar.xz -> core-image-base-myd-y6ull14x14-20171011084756.rootfs.tar.xz
-rw-r--r-- 1 kevinchen kevinchen 532M Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.ext4
-rw-r--r-- 1 kevinchen kevinchen 7.3K Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.manifest
-rw-r--r-- 1 kevinchen kevinchen 548M Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.sdcard
-rw-r--r-- 1 kevinchen kevinchen 111M Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.tar.bz2
-rw-r--r-- 1 kevinchen kevinchen  64M Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.tar.xz
lrwxrwxrwx 1 kevinchen kevinchen   55 Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14.ext4 -> fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.ext4
lrwxrwxrwx 1 kevinchen kevinchen   59 Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14.manifest -> fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.manifest
lrwxrwxrwx 1 kevinchen kevinchen   57 Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14.sdcard -> fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.sdcard
lrwxrwxrwx 1 kevinchen kevinchen   58 Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14.tar.bz2 -> fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.tar.bz2
lrwxrwxrwx 1 kevinchen kevinchen   57 Oct 11 17:02 fsl-image-qt5-myd-y6ull14x14.tar.xz -> fsl-image-qt5-myd-y6ull14x14-20171011090003.rootfs.tar.xz
-rw-r--r-- 2 kevinchen kevinchen 1.3M Oct 11 16:47 modules--4.1.15-r0-myd-y6ull14x14-20171011084447.tgz
lrwxrwxrwx 1 kevinchen kevinchen   52 Oct 11 16:47 modules-myd-y6ull14x14.tgz -> modules--4.1.15-r0-myd-y6ull14x14-20171011084447.tgz
-rw-r--r-- 2 kevinchen kevinchen  294 Oct 11 17:01 README_-_DO_NOT_DELETE_FILES_IN_THIS_DIRECTORY.txt
lrwxrwxrwx 1 kevinchen kevinchen   26 Oct 11 16:01 u-boot.imx -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Oct 11 16:01 u-boot.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   24 Oct 11 16:01 u-boot.imx-sd -> u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Oct 11 16:01 u-boot-myd-y6ull14x14.imx -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Oct 11 16:01 u-boot-myd-y6ull14x14.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   24 Oct 11 16:01 u-boot-myd-y6ull14x14.imx-sd -> u-boot-sd-2016.03-r0.imx
-rwxr-xr-x 2 kevinchen kevinchen 395K Oct 11 16:01 u-boot-nand-2016.03-r0.imx
-rwxr-xr-x 2 kevinchen kevinchen 343K Oct 11 16:01 u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   51 Oct 11 16:47 zImage -> zImage--4.1.15-r0-myd-y6ull14x14-20171011084447.bin
-rw-r--r-- 2 kevinchen kevinchen 6.2M Oct 11 16:47 zImage--4.1.15-r0-myd-y6ull14x14-20171011084447.bin
-rw-r--r-- 2 kevinchen kevinchen  37K Oct 11 16:47 zImage--4.1.15-r0-myd-y6ull-gpmi-weim-20171011084447.dtb
lrwxrwxrwx 1 kevinchen kevinchen   51 Oct 11 16:47 zImage-myd-y6ull14x14.bin -> zImage--4.1.15-r0-myd-y6ull14x14-20171011084447.bin
lrwxrwxrwx 1 kevinchen kevinchen   56 Oct 11 16:47 zImage-myd-y6ull-gpmi-weim.dtb -> zImage--4.1.15-r0-myd-y6ull-gpmi-weim-20171011084447.dtb

```

Some files are link file in output files.Below is description:

File Name | Usage
------ | ------
*.rootfs.manifest | The list of system include packages
*.rootfs.ext4 | File system package to EXT4 format file
*.rootfs.sdcard | Image can be write to SD card and boot from SD card
*.rootfs.tar.bz2 | File system package to tar.bz2
*.rootfs.tar.xz | File system package to tar.xz
u-boot-emmc-2016.03-r0.imx | u-boot used for booting from  eMMC
u-boot-nand-2016.03-r0.imx | u-boot used for booting from NAND
u-boot-sd-2016.03-r0.imx | u-boot used for booting SD card

## Bitbake common usage

Bitbake arguments | Description
------------ | ----
-c fetch | Download package from predefined of recipe
-c cleanall | Clean all build directory
-c deploy | Deploy image or package to target rootfs
-k | Continue when error occure
-c compile | Recompile image or package
