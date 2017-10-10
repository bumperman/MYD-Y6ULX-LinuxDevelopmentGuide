# 4.14 4G模块 测试


MYD-Y6ULX开发板提供一个4G模块接口。

## 硬件连接

将附带I-PEX接口的天线安装在开发板的J24位置。


系统中已经加入4G模块的驱动，启动后会自动加载相应驱动,驱动加载成功后会出现对应的/dev/ttyUSB*设备，查看：
```
#ls /dev/ttyUSB*

```
* 拨号前的准备，移植pppd。
```
tar -xvf ppp-2.4.5.tar.gz
cd ppp-2.4.5
./configure
#make CC=arm-linux-gnueabihf-gcc

```
编译后生成pppd，进入chat，make编译生成chat。把生成的pppd、pppdump、pppstatus、chat等文件拷贝到arm板/usr/sbin/目录下。

* 拨号
两种方式启动ppp拨号：
一.
