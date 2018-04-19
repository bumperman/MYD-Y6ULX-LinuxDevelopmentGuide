# 6.1 USB Update Method

## Install tool

The NXP provide a manufacture tool called MfgTool, we use MfgTool 2.7.0 version.The MfgTool suppors Windows and Linux system.It is located in directory "03-Tools/ManufactoryTool" of resource package.You can copy and extract it to your work directory.

The MYD-Y6ULX series board support NAND and eMMC flash.The MfgTool also support it on each vbs file.

MYD-Y6ULY2 script list:

Filename | Description
------ | -----
core-image-base-myd-y6ulxy2-ddr512m-emmc4g.vbs | Programming core-image-base into MYD-Y6ULY2 DDR 512MB, eMMC 4GB flash
fsl-image-qt5-myd-y6ulxy2-ddr512m-emmc4g.vbs | Programming fsl-image-qt5 into MYD-Y6ULY2 DDR 512MB, eMMC 4GB flash
core-image-base-myd-y6ulxy2-ddr256m-nand256m.vbs | Programming core-image-base into MYD-Y6ULY2 DDR 256MB, NAND 256MB flash
fsl-image-qt5-myd-y6ulxy2-ddr256m-nand256m.vbs | Programming fsl-image-qt5 into MYD-Y6ULY2 DDR 256MB, NAND 256MB flash

MYD-Y6ULG2 script list:

Filename | Description
------ | -----
core-image-base-myd-y6ulxg2-ddr256m-nand256m.vbs | Programming core-image-base into MYD-Y6ULY2 DDR 256MB, NAND 256MB flash
fsl-image-qt5-myd-y6ulxg2-ddr256m-nand256m.vbs | Programming fsl-image-qt5 into MYD-Y6ULY2 DDR 256MB, NAND 256MB flash
core-image-base-myd-y6ulxg2-ddr512m-emmc4g.vbs | Programming core-image-base into MYD-Y6ULY2 DDR 512MB, eMMC 4GB flash
fsl-image-qt5-myd-y6ulxg2-ddr512m-emmc4g.vbs | Programming fsl-image-qt5 into MYD-Y6ULY2 DDR 512MB, eMMC 4GB flash

## Update steps(follow the sequence):

Below is example with MYD-Y6ULG2 DDR 256MB NAND 256MB board and programming core-image-base system image.

* Change third bit as OFF, four bit as ON on toggle switch(SW1).
* Use USB cable(Type-A to Micro-B) connect to micro usb port(J7) with PC USB port.
* Use DC 12 power supply connect with power jack(J22).
* Double click file "core-image-base-myd-y6ulxg2-ddr256m-nand256m.vbs" under MfgTool directory, then the MfgTool will show the HID device on recognize.
* Click the "Start" button on MfgTool GUI, it will auto download system image to storage of board.

The progress bar will show as green when update finish. While it will show as red if failed.In this case you can view "MfgTool.log" file to get more information.Another way is use USB to TTL cable connect to Debug port(JP1), you can view the serial port output to analysis failed reason after update again.

### Update files on MfgTool

MfgTool update files has two directories, firmware and files.The files directory store files for burn into flash of MYD-Y6ULX board. It's locate in "MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/files/".
The firmware directory store files for burn system.It's locate in "MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/firmware/".You need to update those files when you change flash size or partition offset.

MYD-Y6ULL file list:

Filename | Description
-------- | -----
core-image-base-myd-y6ull14x14.rootfs.tar.bz2 | core-image-base filesystem for MYD-Y6ULY2 
fsl-image-qt5-myd-y6ull14x14.rootfs.tar.bz2 | fsl-image-qt5 filesystem for MYD-Y6ULY2
u-boot-myd-y6ull14x14_emmc-ddr512.imx | MYD-Y6ULY2 uboot support eMMC 4GB，DDR 512MB
u-boot-myd-y6ull14x14_nand-ddr256.imx | MYD-Y6ULY2 uboot support NAND 256MB，DDR 512MB
zImage-myd-y6ull | kernel image for MYD-Y6ULY2
zImage-myd-y6ull-14x14-gpmi-weim.dtb | MYD-Y6ULY2 kernel dts support NAND flash
zImage-myd-y6ull-14x14-emmc.dtb | MYD-Y6ULY2 kernel dts support eMMC flash

MYD-Y6UL file list:

Filename | Description
-------- | -----
core-image-base-myd-y6ul14x14.rootfs.tar.bz2 | core-image-base filesystem for MYD-Y6ULG2
fsl-image-qt5-myd-y6ul14x14.rootfs.tar.bz2 | fsl-image-qt5 filesystem for MYD-Y6ULG2的
u-boot-myd-y6ul14x14_emmc-ddr512.imx | MYD-Y6ULG2 uboot support eMMC 4GB，DDR 512MB
u-boot-myd-y6ul14x14_nand-ddr256.imx | MYD-Y6ULG2 uboot support NAND 256MB，DDR 512MB
zImage-myd-y6ul | kernel image for MYD-Y6ULG2
zImage-myd-y6ul-14x14-gpmi-weim.dtb | MYD-Y6ULG2 kernel dts support NAND flash
zImage-myd-y6ul-14x14-emmc.dtb | MYD-Y6ULG2 kernel dts support eMMC flash

## Boot from NAND

You need power down and change the toggle switch(SW1) to NAND or eMMC boot type.

### MYD-Y6ULX boot NAND Flash

Boot bit | Status
--- | ----
Bit1 | OFF
Bit2 | ON
Bit3 | ON
Bit4 | OFF

### MYD-Y6ULX boot eMMC Flash

Boot bit | Status
--- | ----
Bit1 | OFF
Bit2 | OFF
Bit3 | ON
Bit4 | OFF


Reconnect the power adapter, the board will boot into linux on NAND or eMMC flash。
