# 3.3.1 Yocto构建Linux系统

## 设置repo

```
mkdir ~/bin (this step may not be needed if the bin folder already exists)
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

## 设置Yocto

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

## 构建带Qt5的Image
使用NXP提供的脚本，创建一个工作空间，然后在此空间下构建镜像。

```
DISTRO=myir-imx6ulx-fb MACHINE=mys6ul14x14 source fsl-setup-release.sh build
bitbake fsl-image-qt5
```

## 构建带命令行的Image
第二次构建时，如果是同设备，不需要修改其它文件，直接编译即可。

```
bitbake core-image-base
```

Image名称 | 描述 | 用途
---------- | ------ | -----------------
core-image-minimal | minimal版本的文件系统 | 用于MYS-6ULX的升级或更新系统
core-image-base | base版本的终端更多功能的镜像 | 通用的文件系统
fsl-image-qt5 | 构建基于Qt5的镜像 | 带Qt5的通用文件系统

构建文件系统完成后，会在输出目录下有manifest文件，这个文件里包含了对应文件系统中已安装的软件包。

Yocto第一次构建会需要很长时间，取决于计算机的CPU核心数和硬件读写速度。Yocto建议可以使用八核和SSD硬盘可以加速构建速度。第一次构建完成后会生成缓存，后面修改的构建，时间会减少很多。

檭建完成后在会"tmp/deploy/images/mys6ul14x14/"目录下生成不同的文件，以下是构建后的一个例子：
```
kevinchen@debian:~/mys-imx6ul/fsl-release-yocto/build$ ls -lh tmp/deploy/images/mys6ul14x14/
total 1.8G
-rw-r--r-- 1 blackrose blackrose  56M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.ext4
-rw-r--r-- 1 blackrose blackrose 2.1K Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.manifest
-rw-r--r-- 1 blackrose blackrose  72M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.sdcard
-rw-r--r-- 1 blackrose blackrose  11M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.bz2
-rw-r--r-- 1 blackrose blackrose 7.3M Apr 16 23:05 core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.xz
lrwxrwxrwx 1 blackrose blackrose   57 Apr 16 23:05 core-image-minimal-mys6ul14x14.ext4 -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.ext4
lrwxrwxrwx 1 blackrose blackrose   61 Apr 16 23:05 core-image-minimal-mys6ul14x14.manifest -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.manifest
lrwxrwxrwx 1 blackrose blackrose   59 Apr 16 23:05 core-image-minimal-mys6ul14x14.sdcard -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.sdcard
lrwxrwxrwx 1 blackrose blackrose   60 Apr 16 23:05 core-image-minimal-mys6ul14x14.tar.bz2 -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.bz2
lrwxrwxrwx 1 blackrose blackrose   59 Apr 16 23:05 core-image-minimal-mys6ul14x14.tar.xz -> core-image-minimal-mys6ul14x14-20170416150516.rootfs.tar.xz
-rw-r--r-- 1 blackrose blackrose 780M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.ext4
-rw-r--r-- 1 blackrose blackrose  35K Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.manifest
-rw-r--r-- 1 blackrose blackrose 796M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.sdcard
-rw-r--r-- 1 blackrose blackrose 166M Apr 16 23:08 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.bz2
-rw-r--r-- 1 blackrose blackrose 105M Apr 16 23:09 fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.xz
lrwxrwxrwx 1 blackrose blackrose   52 Apr 16 23:08 fsl-image-qt5-mys6ul14x14.ext4 -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.ext4
lrwxrwxrwx 1 blackrose blackrose   56 Apr 16 23:08 fsl-image-qt5-mys6ul14x14.manifest -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.manifest
lrwxrwxrwx 1 blackrose blackrose   54 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.sdcard -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.sdcard
lrwxrwxrwx 1 blackrose blackrose   55 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.tar.bz2 -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.bz2
lrwxrwxrwx 1 blackrose blackrose   54 Apr 16 23:09 fsl-image-qt5-mys6ul14x14.tar.xz -> fsl-image-qt5-mys6ul14x14-20170416150603.rootfs.tar.xz
-rw-r--r-- 2 blackrose blackrose 657K Apr 16 23:04 modules--4.1.15-r0-mys6ul14x14-20170416150349.tgz
lrwxrwxrwx 1 blackrose blackrose   49 Apr 16 23:04 modules-mys6ul14x14.tgz -> modules--4.1.15-r0-mys6ul14x14-20170416150349.tgz
-rw-r--r-- 2 blackrose blackrose  294 Apr 16 23:07 README_-_DO_NOT_DELETE_FILES_IN_THIS_DIRECTORY.txt
-rwxr-xr-x 2 blackrose blackrose 375K Apr 16 22:53 u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot.imx -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot.imx-emmc -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   24 Apr 16 22:53 u-boot.imx-sd -> u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot-mys6ul14x14.imx -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot-mys6ul14x14.imx-emmc -> u-boot-emmc-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   26 Apr 16 22:53 u-boot-mys6ul14x14.imx-nand -> u-boot-nand-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   24 Apr 16 22:53 u-boot-mys6ul14x14.imx-sd -> u-boot-sd-2016.03-r0.imx
-rwxr-xr-x 2 blackrose blackrose 427K Apr 16 22:53 u-boot-nand-2016.03-r0.imx
-rwxr-xr-x 2 blackrose blackrose 375K Apr 16 22:53 u-boot-sd-2016.03-r0.imx
lrwxrwxrwx 1 blackrose blackrose   48 Apr 16 23:04 zImage -> zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
-rw-r--r-- 2 blackrose blackrose 6.5M Apr 16 23:04 zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
-rw-r--r-- 2 blackrose blackrose  36K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-20170416150349.dtb
-rw-r--r-- 2 blackrose blackrose  37K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-emmc-20170416150349.dtb
-rw-r--r-- 2 blackrose blackrose  37K Apr 16 23:04 zImage--4.1.15-r0-mys-imx6ul-14x14-evk-gpmi-weim-20170416150349.dtb
lrwxrwxrwx 1 blackrose blackrose   48 Apr 16 23:04 zImage-mys6ul14x14.bin -> zImage--4.1.15-r0-mys6ul14x14-20170416150349.bin
lrwxrwxrwx 1 blackrose blackrose   57 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-20170416150349.dtb
lrwxrwxrwx 1 blackrose blackrose   62 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk-emmc.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-emmc-20170416150349.dtb
lrwxrwxrwx 1 blackrose blackrose   67 Apr 16 23:04 zImage-mys-imx6ul-14x14-evk-gpmi-weim.dtb -> zImage--4.1.15-r0-mys-imx6ul-14x14-evk-gpmi-weim-20170416150349.dtb

```

生成的文件中，有一些是链接文件，下面是不同文件的用途：

文件名 | 用途
------ | ----
*.rootfs.manifest | 文件系统内的软件列表
*.rootfs.ext4 | 打包成ext4格式的文件系统
*.rootfs.sdcard | 可直接写入SD卡，从SD卡启动的镜像
*.rootfs.tar.bz2 | 打包成tar.bz2格式的文件系统
*.rootfs.tar.xz | 打包成tar.xz格式的文件系统
u-boot-emmc-2016.03-r0.imx | 适合从eMMC启动的u-boot镜像
u-boot-nand-2016.03-r0.imx | 适合从NAND启动的u-boot镜像
u-boot-sd-2016.03-r0.imx | 适合从SD卡启动的u-boot镜像

## Bitbake常用命令

Bitbake 参数 | 描述
------------ | ----
-c fetch | 从recipe中定义的地址，拉取软件到本地
-c cleanall | 清空整个构建目录
-c deploy | 部署镜像或软件包到目标rootfs内
-k | 有错误发生时也继续构建
-c compile | 重新编译镜像或软件包

