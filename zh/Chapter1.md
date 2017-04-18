# 1 软件资源

MYS-6ULx搭载基于Linux 4.1.15内核的操作系统，提供了丰富的系统资源和软件资源。以下是MYS-6ULx的软件资源列表：

类别 | 名称 | 描述信息 | 源码
---- | ---- | ---- | ----
引导程序 | U-boot | u-boot.imx引导启动程序 | YES
Linux内核 |	Linux 4.1.15 | 基于官方imx_4.1.15_2.0.0_ga版本 | YES
设备驱动 | USB Host | USB Host驱动 | YES
设备驱动 | USB OTG | USB OTG驱动 | YES
设备驱动 | I2C | I2C总线驱动 | YES
设备驱动 | Ethernet | 10/100Mbps以太网驱动 | YES
设备驱动 | MMC | MMC/eMMC/TF卡存储驱动 | YES
设备驱动 | LCD | 显示驱动，支持4寸和7寸液晶屏 | YES
设备驱动 | RTC | 实时时钟驱动 | YES
设备驱动 | Touch | 电容(FT5316)，电阻触摸 | YES
设备驱动 | USART | 串口驱动 | YES
设备驱动 | LED | GPIO LED驱动 | YES
设备驱动 | KEY | GPIO KEY驱动 | YES
文件系统 | Debian rootfs | 基于Debian构建带X11的文件系统 | YES
文件系统 | Yotcto rootfs | 基于Yocto构建带Qt 5.6的文件系统 | YES
文件系统 | Yotcto rootfs | 基于Yocto构建终端型的通用文件系统 | YES
应用程序 | GPIO KEY | GPIO按键指示例程 | YES
应用程序 | GPIO LED | 按键指示灯例程 | YES
应用程序 | NET | TCP/IP Sokect C/S例程 | YES
应用程序 | RTC | 实时时钟例程 | YES
应用程序 | RS485 | RS485例程 | YES
应用程序 | RS232 | RS232例程 | YES
应用程序 | Audio | Audio例程 | YES
应用程序 | LCD | 显示屏例程 | YES
应用程序 | Amazon AVS demo | 基于Amazon AVS的语音互动demo | YES
编译工具链 | Cross compiler | Linaro GCC 4.9 Hardfloat | BINARY
编译工具链 | Cross compiler | Yocto GCC 5.3 Hardfloat | BINARY

表1-1软件资源列表
