# 3.3.1 Yocto构建Linux系统

本节适合需要对文件系统进行深度定制的开发者，希望从Yocto构建出符合MYD-Y6ULX系列开发板的文件系统，同时基于它的定制需求。初次体验使用或无特殊需要的开发者可以直接使用MYD-Y6ULX已经提供的文件系统。

由于Yocto构建前需要下载文件系统中所有软件包到本地，为了快速构建，MYD-Y6ULX已经把相关的软件打包好，可以直接解压使用，减少重复下载的时间。

注意：构建Yocto不需要加载工具链环境变量，请创建新shell或打开新的终端窗口。

## MYD-Y6ULX提供的Yocto

解压Yocto源码包，同时解压Yocto-downloads.tar.xz软件包至Yocto目录下。Yocto-downloads.tar.xz是把Yocto构建中用到的第三方软件包打包，免除开发者再次下载花费的时间。

注意：由于Yocto-downloads.tar.xz文件较大，无法与MYD-Y6ULX打包在同一文件内，请访问网页下载: [http://down.myir-tech.com/MYD-Y6ULX/](http://down.myir-tech.com/MYD-Y6ULX/)。文件名为Yocto-downloads.tar.xz。

```
cd $DEV_ROOT
tar xvf 04-Source/fsl-release-yocto.tar.xz
tar xvf 04-Source/Yocto-downloads.tar.xz -C fsl-release-yocto
```

还需要将Linux内核和U-Boot代码放在用户家目录下，方便开发和Yocto编译。

```
tar xvf 04-Source/MYiR-iMX-Linux.tar.gz -C ~/
tar xvf 04-Source/MYiR-iMX-uboot.tar.gz -C ~/
```

## 初始化Yocto构建目录

使用NXP提供的fsl-setup-release.sh脚本，会创建一个工作空间，然后在此空间下构建镜像。执行脚本后会先要求阅读并同意版权声明后才会进入构盡过目录。同时，脚本会默认创建并进入build目录。如果需要特定目录名称，可以使用-b参数，如"-b myir"。
MACHINE可选参数为"myd-y6ull14x14"或"myd-y6ul14x14"，分别对应MYD-Y6ULL和MYD-Y6UL开发板。

```
cd fsl-release-bsp
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

build/conf目录下是当前构建的配置文件。上面在初始化后，就可以构建适合"myd-y6ull14x14"的镜像了。

## 构建GUI Qt5版的系统
第一次构建时，会需要很长时间，请耐心等待。

```
bitbake fsl-image-qt5
```

## 构建非GUI版的系统

第二次构建时，如果是同设备，不需要修改其它文件，直接编译即可。

```
bitbake core-image-base
```

Image名称 | 描述 | 用途
---------- | ------ | -----------------
core-image-minimal | minimal版本的文件系统 | 用于MYD-Y6ULX的最小系统
core-image-base | base版本的终端更多功能的镜像 | 通用的文件系统
fsl-image-qt5 | 构建基于Qt5的镜像 | 带Qt5的通用文件系统

构建文件系统完成后，会在输出目录下有manifest文件，这个文件里包含了对应文件系统中已安装的软件包。

Yocto第一次构建会需要很长时间，取决于计算机的CPU核心数和硬件读写速度。Yocto建议可以使用八核和SSD硬盘可以加速构建速度。第一次构建完成后会生成缓存，后面修改的构建，时间会减少很多。

檭建完成后在会"tmp/deploy/images/myd-y6ull14x14/"目录下生成不同的文件，以下是构建后的一个例子：
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

生成的文件中，有一些是链接文件，下面是不同文件的用途：

文件名 | 用途
------ | ----
*.rootfs.manifest | 文件系统内的软件列表
*.rootfs.ext4 | 打包成ext4格式的文件系统
*.rootfs.sdcard | 可直接写入SD卡，从SD卡启动的镜像
*.rootfs.tar.bz2 | 打包成tar.bz2格式的文件系统
*.rootfs.tar.xz | 打包成tar.xz格式的文件系统
u-boot-sd-2016.03-r0.imx | 适合从SD启动的u-boot镜像
u-boot-nand-2016.03-r0.imx | 适合从NAND启动的u-boot镜像

## Bitbake常用命令

Bitbake 参数 | 描述
------------ | ----
-c fetch | 从recipe中定义的地址，拉取软件到本地
-c cleanall | 清空整个构建目录
-c deploy | 部署镜像或软件包到目标rootfs内
-k | 有错误发生时也继续构建
-c compile | 重新编译镜像或软件包

更多Yocto使用方法，请参考NXP官方Yocto使用文档《i.MX Yocto Project User's Guide》。
