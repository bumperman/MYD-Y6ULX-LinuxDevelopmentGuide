# 1 软件资源

MYD-Y6ULX搭载基于Linux 4.1.15内核的操作系统，提供了丰富的系统资源和软件资源。部分资源需要配合相应的扩展模块才能使用。以下是软件资源列表：

类别 | 名称 | 描述信息 | 源码
---- | ---- | ---- | ----
引导程序 | U-boot | u-boot.imx引导启动程序 | YES
Linux内核 |	Linux 4.1.15 | 基于官方imx_4.1.15_2.0.0_ga版本 | YES
设备驱动 | USB Host | USB Host驱动 | YES
设备驱动 | USB OTG | USB OTG驱动 | YES
设备驱动 | I2C | I2C总线驱动 | YES
设备驱动 | Ethernet | 10/100Mbps以太网驱动 | YES
设备驱动 | MMC | MMC/eMMC/TF卡存储驱动 | YES
设备驱动 | LCD | 显示驱动，支持4.3寸和7寸液晶屏 | YES
设备驱动 | RTC | 实时时钟驱动 | YES
设备驱动 | Touch | 电容(FT5316)，电阻触摸 | YES
设备驱动 | USART | 串口驱动 | YES
设备驱动 | LED | GPIO LED驱动 | YES
设备驱动 | KEY | GPIO KEY驱动 | YES
设备驱动 | Audio | WM8904驱动 | YES
设备驱动 | CAN bus | CAN总线驱动 | YES
设备驱动 | RS485 | RS485总线驱动 | YES
设备驱动 | Camera | OV2659驱动 | YES
设备驱动 | WiFi | USI WM-N-BM-02(BCM43362)，使用MMC驱动 | YES
设备驱动 | LTE模块 | 仅支持移远EC20，使用USB驱动 | YES
文件系统 | Yotcto rootfs | 基于Yocto构建带Qt 5.6的文件系统 | YES
文件系统 | Yotcto rootfs | 基于Yocto构建终端型的通用文件系统 | YES
应用程序 | GPIO KEY | GPIO按键指示例程 | YES
应用程序 | GPIO LED | 按键指示灯例程 | YES
应用程序 | NET | TCP/IP Sokect C/S例程 | YES
应用程序 | RTC | 实时时钟例程 | YES
应用程序 | RS232 | RS232例程 | YES
应用程序 | Audio | Audio例程 | YES
应用程序 | LCD | 显示屏例程 | YES
编译工具链 | Cross compiler | Linaro GCC 4.9 Hardfloat | BINARY
编译工具链 | Cross compiler | Yocto GCC 5.3 Hardfloat | BINARY

表1-1软件资源列表
