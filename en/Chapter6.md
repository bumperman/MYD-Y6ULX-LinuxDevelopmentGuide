# 6 System update

## Installing tool

The programming tool is provided by Atmel Corporation SAM-BA 3.1.4 version, CD-ROM path '03-Tools\SAM-BA' directory, supports Windows and Linux operating system, Linux version has 32bit and 64bit version.

When decompression is done, can be exported to the PATH variable.Set up after pass -v parameter, if the version of information output, that is successfully. If fails, please check the path.

```
tar xvf sam-ba_3.1.4-linux_x86_64.tar.gz
export PATH=$PATH:~/sam-ba_3.1.4
sam-ba -v
SAM-BA Command Line Tool v3.1.4
Copyright 2015-2016 ATMEL Corporation
```

## Programming Steps

### Connect the development board

Connect the development board. Specific steps are as follows (order can not be reversed):

* Set the power switch (J2) to the USB side.
* Use a mini-USB cable to connect the PC to the USB device port(J18).
* Press the BOOT_DIS(K4) button, click the RESET(K1) button at the same time, keep BOOT_DIS pressed for 2 ~ 5 seconds, the CPU enters SAM-BA Monitor mode, then release the BOOT_DIS button. The first time to connect the development board when the PC prompts to install the usb driver, then select the SAM-BA installation directory under the relevant location can be installed as shown.
* Check the ttyACM0 device, indicating that the chip is in SAM-BA Monitor mode, next you can programming system

View the SAM-BA mode serial port under Linux:
```
ls /dev/ttyACM0
/dev/ttyACM0
```

View the SAM-BA mode serial port under Windows:
Open the computer management window within the Device Manager item, the new recognized serial device in right panel.

### Auto programming system

Note: If you have inserted SD card, please remove the SD card before downloading, otherwise there may be programming error.

NAND Flash boot mode: AT91Bootstrap + U-Boot + zImage + dtb + rootfs in NAND Flash
```
sam-ba -x demo_linux_nand.qml
```
