# 6 系统更新

MYS-6ULX系列板的系统更新使用两种方法，MfgTool更新和SD卡更新。

## MfgTool更新系统

### 安装工具

烧写工具是由NXP公司提供的MfgTool 2.7.0版本，光盘中路径"03-Tools/ManufactoryTool"目录下，支持Windows和Linux操作系统。解压后的目录中有多个vbs文件，这些是配置好的烧写脚本。执行后即可启动MfgTool程序。

### 更新步骤如下(顺序不可颠倒):

* 拨动启动拨码开关(SW1)的第3位为ON，第4位为OFF。
* 使用mini-USB线连接PC机USB端口与开发板
* 双击MfgTool目录下的"mfgtool2-yocto-mx6ul-evk-nand.vbs"文件，此时可以看到MfgTool界面已识别到开发板。
* 点击MfgTool界面上的"Start"按钮，MfgTool就开始自动更新系统至板载存储设备。

更新成功后底部的总进度条会显示为绿色。若失败则为红色时，可以查看"MfgTool.log"文件的错误提示信息。或者使用USB转TTL串口线连接至JP1，再重新更新系统，就可以从串口查看更新过程并分析失败的原因。

### 更新MfgTool

MfgTool的文件更新有两个部分，firmware和files。files目录下为烧写的目标镜像文件，路径为"MYS-6ULX-mfgtools/Profiles/Linux/OS Firmware/files/"。
firmware是烧写系统的镜像文件，路径为"MYS-6ULX-mfgtools/Profiles/Linux/OS Firmware/firmware/"。当更新系统的分区大小或烧写方式时才需要更新firmware中的文件。

files目录下的文件说明：

文件名 | 描述
---- | -----
imx6ull-rootfs_nogpu.tar.bz2 | MYS-6ULX-IND 文件系统
imx6ul-rootfs_nogpu.tar.bz2 | MYS-6ULX-IoT 文件系统
u-boot-imx6ul14x14evk_emmc.imx | MYS-6ULX-IND 支持eMMC的uboot
u-boot-imx6ul14x14evk_nand.imx | MYS-6ULX-IND 支持NAND的uboot
u-boot-imx6ull14x14evk_emmc.imx | MYS-6ULX-IoT 支持eMMC的uboot
u-boot-imx6ull14x14evk_nand.imx | MYS-6ULX-IoT 支持NAND的uboot
zImage | MYS-6ULX-IND 和MYS-6ULX-IoT的内核镜像
zImage-imx6ul-14x14-evk-emmc.dtb | MYS-6ULX-IND支持eMMC的设备树文件
zImage-imx6ul-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IND支持NAND的设备树文件
zImage-imx6ull-14x14-evk-emmc.dtb | MYS-6ULX-IoT支持eMMC的设备树文件
zImage-imx6ull-14x14-evk-gpmi-weim.dtb | MYS-6ULX-IND支持NAND的设备树文件


## Micro SD卡更新系统

由于i.MX6ULL/i.MX6UL烧写bootloaer时需要使用kobs-ng工具添加头部信息，需要在操作系统上才可以烧写。
这里提供了两个sdcard后缀的镜像文件，分别对应MYS-6ULX-IoT和MYS-6ULX-IND开发板。sdcard文件是包含分区结构的镜像文件，有两个分区，第一分区为FAT格式，里面有一个最小化Linux系统和更新的目标镜像文件。第二个分区是EXT4格式，作为最小化Linux的文件系统，包含更新脚本。

sdcard镜像文件需要使用特殊的磁盘操作工具才可以写入Micro SD卡内，Linux系统用户可以直接使用dd命令，Windows系统用户使用Win32ImageWriter工具。

### 制做支持SD更新的镜像

若对系统Linux kernel，U-Boot或者Yocto有修改，需要使用工具将这些二进制文件更新的开发板上。MYS-6ULX开发板提供了一个可以制做SD更新镜像的工具MYS-6ULX-mkupdate-sdcard，存放在04-Tools/ManufactoryTool目录。解压后就可以开始制做镜像了。

```
sudo ./build-sdcard.sh -p mys6ull -n -d mfgimages-mys-imx6ul-ddr256m-nand256m
```

build-sdcard.sh提供了四种参数：
* '-p' 表示平台，可用参数为"mys6ull"代表MYS-6ULX-IOT和"mys6ul"代表MYS-6ULX-IND
* '-n' 表示板上存储芯片是NAND
* '-e' 表示板上存储芯片是eMMC
* '-d' 表示更新文件的目录

注意：'-n'和'-e'不能同时使用，只能使用一种。

运行结束后会生成一个sdcard后缀的文件，如'mys6ull-update-nand-20170825150819.rootfs.sdcard'。

### 制做可更新系统的SD卡

MYS-6ULX资源包内提供了用于更新系统的sdcard镜像文件，可以直接使用，也可以使用上一步制做的sdcard文件。
有了用于更新的SD卡镜像文件，就可以把镜像文件写入到SD卡。为了方便使用，建议把Micro SD插入USB读卡器，再插入电脑USB端口。

* Linux系统

通常Linux下的存储设备名为"sd[x][n]"形式，x表示第几个存储设备，一般使用字母a~z表示。n表示存储设备的分区，一般使用数字，从1开始。插入后可以使用"dmesg | tail"命令查看新设备的设备名称。这里以"/dev/sdb"设备为例，sdb后面不写任务分区数字。

```
sudo dd if=mys6ull-update.sdcard of=/dev/sdb conv=fsync
```

写入的速度与USB和Micro SD卡的速率有关，如果对速度有要求，建议选用更高速度等级的Micro SD存储卡。

* Windows系统

Windows用户可以使用Win32DiskImager工具把sdcard镜像写入Micro SD里。工具在"03-Tools"目录下，解压后，双击"Win32DskImager.exe"应用程序。启动后的界面中，右侧的"Device"是选择要写入的设备盘符。左侧的"Image File"是选择将要写的镜像文件，点击旁边的文件夹图标，选中要写入的文件即可(注意：文件选择对话框中默认是过滤"*.img"文件，切换成"*.*"，就可以显示到sdcard后缀的文件)。

写入前请再次确认目标磁盘和文件是否正确，避免写入到系统磁盘，损坏Windows系统分区。

![Win32DiskImage写入镜像](image/6-1.png)

等待进度条结束后，就可以拔出USB读卡器。

把制做好的Micro SD卡插入开发板的卡槽(J5)，启动位拨码开关(SW1)配置为SDCARD启动方式，如下：

启动位 | 状态 
--- | ----
Bit1 | OFF
Bit2 | ON
Bit3 | OFF
Bit4 | ON

连接USB转TTL串口线至调试口(JP1)，配置好电脑端的串口终端软件，连接USB数据线至USB OTG端口(J7)作为电源(也可以使用直接电源连接至J1接口)。通过串口可以看到系统从Micro SD卡启动，并执行更新脚本，把镜像写入NAND存储芯片内。

也可以通过用户LED灯(D12)来判断当前更新状态，更新中为闪烁状态，更新成功后会常亮，失败则会熄灭。

## 切换为NAND启动方式

两种方式重更新完成后断电，配置启动位拨码开关为NAND启动方式，如下：

启动位 | 状态 
--- | ----
Bit1 | ON
Bit2 | OFF
Bit3 | OFF
Bit4 | ON

再次连接电源，开发板即可以从NAND启动系统了。

