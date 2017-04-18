# 1 Software Resource

MYD-JA5D2X supports the Linux kernel 4.1 version, and provides a rich hardware resource and software resource. 

Below is MYD-JA5D2X software resource table:

Categary | Name | Description | Source
---- | ---- | ---- | ----
Bootloader | AT91Bootstrap | First level boot | YES
Bootloader | U-boot | Second level boot | YES
Linux kernel |	Linux 4.1 | supports DeviceTree | YES
Driver | USB Host | USB Host | YES
Driver | USB Device | USB Device | YES
Driver | I2C(TWI) | I2C-dev | YES
Driver | Ethernet |  | YES
Driver | MMC | MMC/SDIO/TF Card | YES
Driver | LCD | Supports 4.3inch and 7.0 inch | YES
Driver | RTC | Read/write real date time | YES
Driver | Touch Panel | Supports Capacity and Resistive touch panel | YES
Driver | Button | GPIO key | YES
Driver | USART | serial port driver | YES
Driver | LED | GPIO LED | YES
Driver | KEY | GPIO KEY | YES
Driver | WatchDog | WatchDog driver | YES
Driver | EERPOM | U15 of core board | YES
Driver | ADC | ADC Driver | YES
Driver | PWM | PWM Driver | YES
FileSystem | Buildroot rootfs | Uses Buildroot with Qt 5.6 | YES
FileSystem | Yotcto rootfs | Uses Yocto with Qt 5.6 | BINARY
Application | GPIO KEY | Reads the GPIO key code value demo  | YES
Application | GPIO LED | Operation the GPIO LED demo | YES
Application | NET | Uses TCP/IP Sokect API, support Client and Server demo | YES
Application | RTC | Read/write real date time demo | YES
Application | I2C(TWI) | Read/write date from I2C EEPROM chip demo | YES
Application | RS485 | Read/write RS485 port demo | YES
Application | RS232 | Read/write RS232 port demo | YES
Application | Audio | Audio play/capture demo | YES
Application | Framebuffer | LCD test program | YES
Toolchain | Cross compiler | Linaro GCC 4.9 Hardfloat | BINARY
Table1-1 Software Resource
