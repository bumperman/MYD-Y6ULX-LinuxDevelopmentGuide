# 3.3.1 Yocto构建Linux系统

本节适合需要对文件系统进行深度定制的开发者，希望从Yocto构建出符合MYS-6ULX系列开发板的文件系统，同时基于它的定制需求。初次体验使用或无特殊需要的开发者可以直接使用MYS-6ULX已经提供的文件系统。

由于Yocto构建前需要下载文件系统中所有软件包到本地，为了快速构建，MYS-6ULX已经把相关的软件打包好，可以直接解压使用，减少重复下载的时间。

这里提供了两种方式使用Yocto:

* 使用由MYS-6ULX资源包中的Yocto和相关文件
* 从NXP官网下载Yocto

初次使用Yocto的用户，推荐使用第一种方式。

## MYS-6ULX提供的Yocto

解压Yocto源码包，同时解压Yocto-downloads.tar.xz软件包至Yocto目录下。Yocto-downloads.tar.xz是把MYS-6ULX构建中用到的第三方软件包打包，免除用户再次下载。

注意：由于Yocto-downloads.tar.xz文件较大，无法与MYS-6ULX打包在同一文件内，请访问网页下载: http://down.myir-tech.com/MYS-6ULX/。

```
cd $DEV_ROOT
tar xvf fsl-release-yocto.tar.xz
tar xvf Yocto-downloads.tar.xz -C $DEV_ROOT/fsl-release-bsp
cd fsl-release-bsp
```

还需要将Linux内核和U-Boot代码放在用户家目录下，方便开发和Yocto编译。

```
mkdir ~/MYS-6ULX-Linux
mkdir ~/MYS-6ULX-uboot
tar xvf $DEV_ROOT/04-Source/linux-4.1.15.tar.gz -C ~/MYS-6ULX-Linux
tar xvf $DEV_ROOT/04-Source/u-boot-2016.03.tar.gz -C ~/MYS-6ULX-uboot
```

## NXP官方提供的Yocto

Yocto下的项目比较多，为了便于管理使用与Android相同的代码管理工具repo。通过repo下载代码前，需要配置好git的用户名和邮箱地址。然后使用repo的命令从NXP官方仓库下载代码

* 设置repo

```
mkdir ~/bin (this step may not be needed if the bin folder already exists)
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

* 设置Yocto

```
git config --global user.name "Your Name"
git config --global user.email "Your email address"
```

```
cd $DEV_ROOT
mkdir fsl-release-bsp
cd fsl-replease-bsp
repo init -u git://git.freescale.com/imx/fsl-arm-yocto-bsp.git -b imx-4.1-krogoth
repo sync
```

同步完成后，需要把meta-myir-imx6ulx拷贝到fsl-release-bsp/source目录下。同时，在后面的初始化构建目录后，还需要在conf/bblayers.conf中添加BBLAYERS += " ${BSPDIR}/sources/meta-myir-imx6ulx "到最后行。

也需要将Linux内核和U-Boot代码放在用户家目录下，方便开发和Yocto编译。

```
mkdir ~/MYS-6ULX-Linux
mkdir ~/MYS-6ULX-uboot
tar xvf $DEV_ROOT/04-Source/linux-4.1.15.tar.gz -C ~/MYS-6ULX-Linux
tar xvf $DEV_ROOT/04-Source/u-boot-2016.03.tar.gz -C ~/MYS-6ULX-uboot
```

## 初始化Yocto构建目录

使用NXP提供的fsl-setup-release.sh脚本，会创建一个工作空间，然后在此空间下构建镜像。执行脚本后会先要求阅读并同意版权声明后才会进入构盡过目录。同时，脚本会默认创建并进入build目录。如果需要特定目录名称，可以使用-b参数，如"-b myir"。
这里的MACHINE参数有两种设备，"mys6ull14x14"对应于MYS-6ULX-IoT和"mys6ul14x14"对应于MYS-6ULX-IND版本。

```
DISTRO=myir-imx-fb MACHINE=mys6ul14x14 source fsl-setup-release.sh
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

build/conf目录下是当前构建的配置文件。上面在初始化时，构建适合"mys6ul14x14"的镜像，也可以在local.conf文件中修改MACHINE变量来构建适合"mys6ull14x14"的镜像。Yocto支持在同一个构建任务下构建多个设备。

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
core-image-minimal | minimal版本的文件系统 | 用于MYS-6ULX的升级或更新系统
core-image-base | base版本的终端更多功能的镜像 | 通用的文件系统
fsl-image-qt5 | 构建基于Qt5的镜像 | 带Qt5的通用文件系统

构建文件系统完成后，会在输出目录下有manifest文件，这个文件里包含了对应文件系统中已安装的软件包。

Yocto第一次构建会需要很长时间，取决于计算机的CPU核心数和硬件读写速度。Yocto建议可以使用八核和SSD硬盘可以加速构建速度。第一次构建完成后会生成缓存，后面修改的构建，时间会减少很多。

檭建完成后在会"tmp/deploy/images/mys6ul14x14/"或"tmp/deploy/images/mys6ull14x14/"目录下生成不同的文件，以下是构建后的一个例子：
```
kevinchen@dev-machine:~/mys-imx6ul/fsl-release-yocto/build$ ls -lh tmp/deploy/images/mys6ul14x14/
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

## Bitbake常用命令

Bitbake 参数 | 描述
------------ | ----
-c fetch | 从recipe中定义的地址，拉取软件到本地
-c cleanall | 清空整个构建目录
-c deploy | 部署镜像或软件包到目标rootfs内
-k | 有错误发生时也继续构建
-c compile | 重新编译镜像或软件包

更多Yocto使用方法，请参考NXP官方Yocto使用文档《i.MX Yocto Project User's Guide》。
