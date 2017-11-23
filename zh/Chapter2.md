# 2 部署开发环境

开发前需要PC安装好Linux操作系统，推荐使用Ubuntu 16.04 64bit发行版，连接网线并配置好网络，后续操作需要连接互联网安装或下载相关软件包。

## 开发板与计算机连接

1. 计算机使用USB转TTL串口转接线与开发板的DEBUG串口(JP1)连接
2. 运行串口调试应用程序，并选择对应的串口设备

计算机端的串口配置参数如下：

* 波特率：115200
* 数据位: 8bit
* 校验方式：None
* 停止位：1bit
* 流控：Disable


<img src="image/2-1.png" width="640" height="640" />

图2-1 MYC-Y6ULX 正面图

![](image/2-2.png)
图2-2 MYD-Y6ULX 正面图

## 安装必备软件包

```
sudo apt-get install build-essential git-core libncurses5-dev \
flex bison texinfo zip unzip zlib1g-dev gettext u-boot-tools \
g++ xz-utils mtd-utils gawk diffstat gcc-multilib python git \
make gcc g++ diffstat bzip2 gawk chrpath wget cpio texinfo
```

## 建立工作目录

建立工作目录，方便设置统一的环境变量路径。拷贝产品光盘中的源码到工作目录下，同时设置DEV_ROOT变量，方便后续步骤的路径访问。

```
mkdir -p ~/MYD-Y6ULX-devel
export DEV_ROOT=~/MYD-Y6ULX-devel
cp -r <DVDROM>/02-Images $DEV_ROOT
cp -r <DVDROM>/03-Tools $DEV_ROOT
cp -r <DVDROM>/04-Source $DEV_ROOT
```

## 配置编译工具

- Linaro交叉编译器: gcc version 4.9.3 20141031 (prerelease) (Linaro GCC 2014.11)
- Yocto交叉编译器: gcc version 5.3.0 (GCC)

这里有两个编译器，一个是Linaro提供，另一个是由Yocto构建的，建议使用Yocto提供的，以便和文件系统统一。

### Linaro编译器

```
cd $DEV_ROOT
tar -xvjf 03-Tools/Toolchain/gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf.tar.xz
export PATH=$PATH:$DEV_ROOT/gcc-linaro-4.9-2014.11-x86_64_arm-linux-gnueabihf/bin
export CROSS_COMPILE=arm-linux-gnueabihf-
export ARCH=arm
```
执行完上述命令后输入"arm-linux-gnueabihf-gcc --version"，若有输出版本信息，说明设置成功，以上设置只对当前终端有效。如需永久修改，请修改用户配置文件。

```
$ arm-linux-gnueabihf-gcc --version

arm-linux-gnueabihf-gcc (Linaro GCC 2014.11) 4.9.3 20141031 (prerelease)
Copyright (C) 2014 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

### Yocto编译工具链

Yocto提供的工具链有两种，一种是底层开发的meta-toolchain，另一种是用于应用开发的工具链。前者和Linaro类似，后者包含应用开发中的相关库，可以直接使用pkg-config工具来解决头文件或库文件的依赖关系。MYD-Y6ULX的资源包中有提供两种工具链。

工具链文件名 | 描述
------------ | -----
myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh | fsl-image-qt5系统的应用工具链
myir-imx-fb-glibc-x86_64-core-image-base-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh | core-image-base系统的应用工具链
myir-imx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh | meta-toolchain基础工具链

Yocto编译器是以SDK工具包方式来提供，需要先安装SDK包后，才可以使用。安装方法如下：

以普通用户权限执行shell脚本，运行中会提示安装路径，默认在/opt目录下，同时会提示输入用户密码以便有写入目录的权限。安装完成后，可以使用"source"或"."命令加载工链接环境到当前终端。

例子把应用开发工具链安装在了/opt/myir-imx6ulx-fb/4.1.15-2.0.1目录下。

```
./myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh 
Freescale i.MX Release Distro SDK installer version 4.1.15-2.0.1
================================================================
Enter target directory for SDK (default: /opt/myir-imx-fb/4.1.15-2.0.1): 
/opt/myir-imx6ulx-fb/4.1.15-2.0.1                                        
Do You are about to install the SDK to "/opt/myir-imx6ulx-fb/4.1.15-2.0.1". Proceed[Y/n]? Y
[sudo] password for kevinchen: 
Extracting SDK..................................................
................................................................
...............done
Setting it up...done
SDK has been successfully set up and is ready to be used.
Each time you wish to use the SDK in a new shell session, you ne
ed to source the environment setup script e.g.
. /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-poky-linux-gnueabi

```
验证SDK工具链是否安装正确，先使用"source"命令加载Yocto的环境配置文件，然后查看编译器版本。
```
source /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-poky-linux-gnueabi
arm-poky-linux-gnueabi-gcc --version

arm-poky-linux-gnueabi-gcc (GCC) 5.3.0
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

同样方法请自行安装底层开发的工具链meta-toolchain。安装两个工具链，请指定不同目录，请勿使用相同目录，出现文件相互覆盖情形。
