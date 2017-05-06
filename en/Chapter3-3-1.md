# 3.3.1 Yocto build Linux system

This section suite for developer on customize file system.If you just want to use it, please use the prebuilt file system.

The Yocto needs download all third software packages from internet.In order to build more speedly, MYS-6ULX also support a full package, you could not download again.

Below has two ways to use Yocto:

* Using MYS-6ULX full package
* Using NXP supports Yocto and config it for MYS-6ULX

If you the first time hear about Yocto, recommend use the first way

## MYS-6ULX support full Yocto package

Extract Yocto source package, and extract the Yocto-downloads.tar.xz into Yocto source direcotry.The Yocto-downloads.tar.xz includes all packages when building MYS-6ULX from Yocto.

Attention: The Yocto-downloads.tar.xz file is more large, it does not include in MYS-6ULX iso file.Please visit and download it from http://d.myirtech.com/MYS-6ULX.

```
cd $DEV_ROOT
tar xvf 04-Source/fsl-release-yocto.tar.xz
tar xvf 04-Source/Yocto-downloads.tar.xz -C fsl-release-bsp
cd fsl-release-bsp
```

Last, also needs put the kernel and u-boot source into your home directory in linux.It will be fetch with Yocto.

```
cd $DEV_ROOT
mkdir ~/MYS-6ULX-Linux
mkdir ~/MYS-6ULX-uboot
tar xvf 04-Source/linux-4.1.15.tar.gz -C ~/MYS-6ULX-Linux
tar xvf 04-Source/u-boot-2016.03.tar.gz -C ~/MYS-6ULX-uboot
```

## NXP support Yocto

Yocto has many sub-porjects, so it use repo tool to manage those projects.You need configure the git and download Yocto from NXP source code repository.

* Setting repo

```
mkdir ~/bin (this step may not be needed if the bin folder already exists)
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

* Setting Yocto

```
git config --global user.name "Your Name"
git config --global user.email "Your mail"
```

```
cd $DEV_ROOT
mkdir fsl-release-bsp
cd fsl-replease-bsp
repo init -u git://git.freescale.com/imx/fsl-arm-yocto-bsp.git -b imx-4.1-krogoth
repo sync
```

When the sync complete, you need copy the meta-myir-imx6ulx to fsl-release-bsp/source directory.On next steps, you need add next line to conf/bblayers.conf file.
```
BBLAYERS += " ${BSPDIR}/sources/meta-myir-imx6ulx "
```

Also, needs put the kernel and u-boot source into your home directory in linux.It will be fetch with Yocto.

```
mkdir ~/MYS-6ULX-Linux
mkdir ~/MYS-6ULX-uboot
tar xvf $DEV_ROOT/04-Source/linux-4.1.15.tar.gz -C ~/MYS-6ULX-Linux
tar xvf $DEV_ROOT/04-Source/u-boot-2016.03.tar.gz -C ~/MYS-6ULX-uboot
```

## Build system image with Qt5 package
Use script by NXP supported, create a workspace directory, and Yocto will build all under it.
MYS-6ULX has two types board, "mys6ull14x14" is MYS-6ULX-IoT and "mys6ul14x14" is MYS-6ULX-IND.

```
DISTRO=myir-imx-fb MACHINE=mys6ul14x14 source fsl-setup-release.sh -b build
bitbake fsl-image-qt5
```

## Build system iamge with full command line packages
You doesn't need to modify any file, just let Yocto to build it.

```
bitbake core-image-base
```

Image Name | Description | Used for
---------- | ------ | -----------------
core-image-minimal | minimal file system | used for MYS-6ULX to update system
core-image-base | base file system has more command line feature | full commnand line system, no GUI
fsl-image-qt5 | system use Qt5 as GUI | used for graphics requirment

After build process finish, it will output manifest file.This file has each package name and version be installed to target file system.

The first build process of Yocto will take more time, this depend on your PC cpu core number and RAM size. The Yocto recommend use eight core CPU and SSD hardware to impove build speed. Another way, the Yocto will generate cache after first build, the next build process also save more time for you.

All output files are in "tmp/deploy/images/mys6ul14x14/" directory after build complete. Below as example:

```
kevinchen@debian:~/mys-imx6ul/fsl-release-yocto/build$ ls -lh tmp/deploy/images/mys6ul14x14/
total 1.8G
-rw-r--r-- 1 kevinchen kevinchen  56M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.ext4
-rw-r--r-- 1 kevinchen kevinchen 2.1K Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.manifest
-rw-r--r-- 1 kevinchen kevinchen  72M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.sdcard
-rw-r--r-- 1 kevinchen kevinchen  11M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.bz2
-rw-r--r-- 1 kevinchen kevinchen 7.3M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.xz
lrwxrwxrwx 1 kevinchen kevinchen   57 Apr 16 23:05 core-image-minimal-mys6ul14x14.ext4 -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.ext4
lrwxrwxrwx 1 kevinchen kevinchen   61 Apr 16 23:05 core-image-minimal-mys6ul14x14.manifest -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.manifest
lrwxrwxrwx 1 kevinchen kevinchen   59 Apr 16 23:05 core-image-minimal-mys6ul14x14.sdcard -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.sdcard
lrwxrwxrwx 1 kevinchen kevinchen   60 Apr 16 23:05 core-image-minimal-mys6ul14x14.tar.bz2 -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.bz2
lrwxrwxrwx 1 kevinchen kevinchen   59 Apr 16 23:05 core-image-minimal-mys6ul14x14.tar.xz -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.xz
-rw-r--r-- 1 kevinchen kevinchen 780M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.ext4
-rw-r--r-- 1 kevinchen kevinchen  35K Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.manifest
-rw-r--r-- 1 kevinchen kevinchen 796M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.sdcard
-rw-r--r-- 1 kevinchen kevinchen 166M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.bz2
-rw-r--r-- 1 kevinchen kevinchen 105M Apr 16 23:09 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.xz
lrwxrwxrwx 1 kevinchen kevinchen   52 Apr 16 23:08 fsl-image-qt5-mys6ul14x14.ext4 -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.ext4
lrwxrwxrwx 1 kevinchen kevinchen   56 Apr 16 23:08 fsl-image-qt5-mys6ul14x14.manifest -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.manifest
lrwxrwxrwx 1 kevinchen kevinchen   54 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.sdcard -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.sdcard
lrwxrwxrwx 1 kevinchen kevinchen   55 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.tar.bz2 -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.bz2
lrwxrwxrwx 1 kevinchen kevinchen   54 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.tar.xz -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.xz
-rw-r--r-- 2 kevinchen kevinchen 657K Apr 16 23:04 modules--4.1.15-r0-mys6ul14x14-20170416150349.tgz
lrwxrwxrwx 1 kevinchen kevinchen   49 Apr 16 23:04 modules-mys6ul14x14.tgz -> modules--4.1.15-r0-mys6ul14x14-20170416150349.tgz
-rw-r--r-- 2 kevinchen kevinchen  294 Apr 16 23:07 README_-_DO_NOT_DELETE_FILES_IN_THIS_DIRECTORY.txt
-rwxr-xr-x 2 kevinchen kevinchen 375K Apr 16 22:53 u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot.imx -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot.imx-emmc -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   24 Apr 16 22:53 u-boot.imx-sd -> u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot-mys6ul14x14.imx -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot-mys6ul14x14.imx-emmc -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   26 Apr 16 22:53 u-boot-mys6ul14x14.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   24 Apr 16 22:53 u-boot-mys6ul14x14.imx-sd -> u-boot-sd-2016.03-r0.imx
-rwxr-xr-x 2 kevinchen kevinchen 427K Apr 16 22:53 u-boot-nand-2016.03-r0.imx
-rwxr-xr-x 2 kevinchen kevinchen 375K Apr 16 22:53 u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 kevinchen kevinchen   48 Apr 16 23:04 zImage -> zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
-rw-r--r-- 2 kevinchen kevinchen 6.5M Apr 16 23:04 zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
-rw-r--r-- 2 kevinchen kevinchen  36K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-20170416150349.dtb
-rw-r--r-- 2 kevinchen kevinchen  37K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-emmc-20170416150349.dtb
-rw-r--r-- 2 kevinchen kevinchen  37K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-gpmi-weim-20170416150349.dtb
lrwxrwxrwx 1 kevinchen kevinchen   48 Apr 16 23:04 zImage-mys6ul14x14.bin -> zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
lrwxrwxrwx 1 kevinchen kevinchen   57 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-20170416150349.dtb
lrwxrwxrwx 1 kevinchen kevinchen   62 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk-emmc.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-emmc-20170416150349.dtb
lrwxrwxrwx 1 kevinchen kevinchen   67 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk-gpmi-weim.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-gpmi-weim-20170416150349.dtb

```

Some files are link file in output files.Below is description:

File Name | Usage
------ | ------
*.rootfs.manifest | The list of system include packages
*.rootfs.ext4 | File system package to EXT4 format file
*.rootfs.sdcard | Image can be write to SD card and boot from SD card
*.rootfs.tar.bz2 | File system package to tar.bz2
*.rootfs.tar.xz | File system package to tar.xz
u-boot-emmc-2016.03-r0.imx | u-boot used for boot from  eMMC
u-boot-nand-2016.03-r0.imx | u-boot used for boot from NAND
u-boot-sd-2016.03-r0.imx | u-boot used for boot SD card

## Bitbake common usage

Bitbake arguments | Description
------------ | ----
-c fetch | Download package from predefined of recipe
-c cleanall | Clean all build directory
-c deploy | Deploy image or package to target rootfs
-k | Continue when error occure
-c compile | Recompile image or package
