# 6.1 USB更新

USB更新方法的烧写工具是由NXP公司提供的MfgTool 2.7.0版本，文件包名为MYD-Y6ULX-mfgtools-20171012.zip，光盘中路径"03-Tools/ManufactoryTool"目录下，支持Windows和Linux操作系统。解压后的目录中有vbs文件，这些是配置好的烧写脚本。执行后即可启动MfgTool程序。

MYD-Y6ULX支持两种Flash存储方式，NAND和eMMC。MfgTool烧写时，选择不同vbs文件即可。

MYD-Y6ULY2烧写脚本列表：

文件名 | 描述
------ | -----
core-image-base-myd-y6ulxy2-ddr512m-emmc4g.vbs | 烧写core-image-base至MYD-Y6ULY2 DDR 512MB, eMMC 4GB配置
fsl-image-qt5-myd-y6ulxy2-ddr512m-emmc4g.vbs | 烧写fsl-image-qt5至MYD-Y6ULY2 DDR 512MB, eMMC 4GB配置
core-image-base-myd-y6ulxy2-ddr256m-nand256m.vbs | 烧写core-image-base至MYD-Y6ULY2 DDR 256MB, NAND 256MB配置
fsl-image-qt5-myd-y6ulxy2-ddr256m-nand256m.vbs | 烧写fsl-image-qt5至MYD-Y6ULY2 DDR 256MB, NAND 256MB配置

MYD-Y6ULG2烧写脚本列表：

文件名 | 描述
------ | -----
core-image-base-myd-y6ulxg2-ddr256m-nand256m.vbs | 烧写core-image-base至MYD-Y6ULY2 DDR 256MB, NAND 256MB配置
fsl-image-qt5-myd-y6ulxg2-ddr256m-nand256m.vbs | 烧写fsl-image-qt5至MYD-Y6ULY2 DDR 256MB, NAND 256MB配置
core-image-base-myd-y6ulxg2-ddr512m-emmc4g.vbs | 烧写core-image-base至MYD-Y6ULY2 DDR 512MB, eMMC 4GB配置
fsl-image-qt5-myd-y6ulxg2-ddr512m-emmc4g.vbs | 烧写fsl-image-qt5至MYD-Y6ULY2 DDR 512MB, eMMC 4GB配置

## 更新步骤如下(顺序不可颠倒)

下面以MYD-Y6ULG2 DDR 256MB NAND 256MB配置的开发板为例，烧写core-image-base系统镜像。

* 切换启动拨码开关(SW1)的第3位为OFF，第4位为ON。
* 使用USB转接线(Type-A转Micro-B)连接PC机USB端口与开发板Micro USB OTG端口(J26)。
* 使用DC 12V电源适配器连接至开发板的电源座(J22)。
* 双击MfgTool目录下的"core-image-base-myd-y6ulg2-ddr256m-nand256m.vbs"，此时可以看到MfgTool界面已识别到开发板。
* 点击MfgTool界面上的"Start"按钮，MfgTool就开始自动更新系统至板载NAND存储芯片。

更新成功后底部的总进度条会显示为绿色。若失败则为红色时，可以查看"MfgTool.log"文件的错误提示信息。或者使用USB转TTL串口线连接至JP1，再重新更新系统，就可以从串口查看更新过程并分析失败的原因。

## 更新MfgTool的文件

如果需要将自己编译的系统镜像文件更新到开发板上时，需要替换MfgTool里面对应的文件。MfgTool的文件更新有两个部分，firmware和files。files目录下为烧写的目标镜像文件，路径为"MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/files/"。
firmware是烧写系统的镜像文件，路径为"MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/firmware/"。当更新系统的分区大小或烧写方式时才需要更新firmware中的文件。

files目录下的文件说明：

MYD-Y6ULL文件列表

文件名 | 描述
---- | -----
core-image-base-myd-y6ull14x14.rootfs.tar.bz2 | MYD-Y6ULY2的core-image-base文件系统
fsl-image-qt5-myd-y6ull14x14.rootfs.tar.bz2 | MYD-Y6ULY2的fsl-image-qt5文件系统
u-boot-myd-y6ull14x14_emmc-ddr512.imx | MYD-Y6ULY2 支持eMMC 4GB，DDR 512MB启动的uboot
u-boot-myd-y6ull14x14_nand-ddr256.imx | MYD-Y6ULY2 支持NAND 256MB，DDR 512MB启动的uboot
zImage-myd-y6ull | MYD-Y6ULY2 的内核镜像
zImage-myd-y6ull-14x14-gpmi-weim.dtb | MYD-Y6ULY2 支持NAND的设备树文件
zImage-myd-y6ull-14x14-emmc.dtb | MYD-Y6ULY2 支持eMMC的设备树文件

MYD-Y6UL文件列表

文件名 | 描述
---- | -----
core-image-base-myd-y6ul14x14.rootfs.tar.bz2 | MYD-Y6ULG2的core-image-base文件系统
fsl-image-qt5-myd-y6ul14x14.rootfs.tar.bz2 | MYD-Y6ULG2的fsl-image-qt5文件系统
u-boot-myd-y6ul14x14_emmc-ddr512.imx | MYD-Y6ULG2 支持eMMC 4GB，DDR 512MB启动的uboot
u-boot-myd-y6ul14x14_nand-ddr256.imx | MYD-Y6ULG2 支持NAND 256MB，DDR 512MB启动的uboot
zImage-myd-y6ul | MYD-Y6ULG2 的内核镜像
zImage-myd-y6ul-14x14-gpmi-weim.dtb | MYD-Y6ULG2 支持NAND的设备树文件
zImage-myd-y6ul-14x14-emmc.dtb | MYD-Y6ULG2 支持eMMC的设备树文件

## 切换为板载Flash启动方式

更新完成后断电，配置启动位拨码开关为板载Flash启动方式，不同存储器的启动位不相同。

### MYD-Y6UL NAND存储版本

启动位 | 状态 
--- | ----
Bit1 | OFF
Bit2 | ON
Bit3 | ON
Bit4 | OFF

### MYD-Y6UL eMMC存储版本

启动位 | 状态 
--- | ----
Bit1 | OFF
Bit2 | OFF
Bit3 | ON
Bit4 | OFF

重新连接电源，开发板即可以从NAND或eMMC启动系统了。

