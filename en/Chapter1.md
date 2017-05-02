# 1 Software Resource

MYS-6ULX serie board supports the Linux kernel version 4.1.15, and provides a rich hardware resource and software resource. 

Below is MYS-6ULX software resource table:

Categary | Name | Description | Source
---- | ---- | ---- | ----
Bootloader | U-boot | u-boot.imx will boot chip to work | YES
Linux kernel |	Linux 4.1.15 | Based on official version imx_4.1.15_2.0.0_ga | YES
Driver | USB Host | USB Host | YES
Driver | USB OTG | USB OTG driver | YES
Driver | I2C | I2C bus driver | YES
Driver | Ethernet | 10/100Mbps ethernet driver | YES
Driver | MMC | MMC/SDIO/TF Card | YES
Driver | LCD | Supports 4.3inch and 7.0 inch | YES
Driver | RTC | Read/write real date time | YES
Driver | Touch Panel | Supports Capacity and Resistive touch panel | YES
Driver | USART | serial port driver | YES
Driver | LED | GPIO LED | YES
Driver | KEY | GPIO KEY | YES
FileSystem | Debian rootfs | Based on Debian build filesystem(include X11 package) | YES
FileSystem | Yotcto rootfs | Based Yocto build filesystem(include Qt 5.6 package) | YES
FileSystem | Yotcto rootfs | Based Yocto build filesystem(Full command line package) | YES
Application | GPIO KEY | Reads the GPIO key code value demo  | YES
Application | GPIO LED | Operation the GPIO LED demo | YES
Application | NET | Uses TCP/IP Sokect API, support Client and Server demo | YES
Application | RTC | Read/write real date time demo | YES
Application | RS232 | Read/write RS232 port demo | YES
Application | Audio | Audio play/capture demo | YES
Application | Framebuffer | LCD test program | YES
Toolchain | Cross compiler | Linaro GCC 4.9 Hardfloat | BINARY
Toolchain | Cross compiler | Yocto GCC 5.3 Hardfloat | BINARY

Table1-1 Software Resource
