# 6 USB Update Method

## Install tool

The NXP provide a manufacture tool called MfgTool, we use MfgTool 2.7.0 version.The MfgTool suppors Windows and Linux system.It is located in directory "03-Tools/ManufactoryTool" of resource package.You can copy and extract it to your work directory.

## Update steps(follow the sequence):

* Change third bit as OFF, four bit as ON on toggle switch(SW1).
* Use USB cable(Type-A to Micro-B) connect to micro usb port(J7) with PC USB port.
* Use DC 12 power supply connect with power jack(J22).
* Double click file "core-image-base-myd-y6ull-nand.vbs" under MfgTool directory, then the MfgTool will show the HID device on recognize.
* Click the "Start" button on MfgTool GUI, it will auto download system image to storage of board.

The progress bar will show as green when update finish. While it will show as red if failed.In this case you can view "MfgTool.log" file to get more information.Another way is use USB to TTL cable connect to Debug port(JP1), you can view the serial port output to analysis failed reason after update again.

### Update files on MfgTool

MfgTool update files has two directories, firmware and files.The files directory store files for burn into flash of MYD-Y6ULX board. It's locate in "MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/files/".
The firmware directory store files for burn system.It's locate in "MYD-Y6ULX-mfgtools/Profiles/Linux/OS Firmware/firmware/".You need to update those files when you change flash size or partition offset.

List of files directory:

FileName | Description
---- | -----
core-image-base-myd-y6ull14x14.rootfs.tar.bz2 | core-image-base file system
u-boot-myd-y6ull14x14evk_nand.imx | Support NAND of uboot for MYD-Y6ULX
zImage-myd-y6ull | Linux kernel image for MYD-Y6ULX
zImage-myd-y6ull-14x14-gpmi-weim.dtb | Support NAND of DeviceTree file for MYD-Y6ULX

## Boot from NAND

You need power down and change the toggle switch(SW1) to NAND boot type when you follow each way from two ways.

Boot bit | Status
--- | ----
Bit1 | OFF
Bit2 | ON
Bit3 | ON
Bit4 | OFF

Reconnect the power adapter, the board will boot into linux on NAND flash。
