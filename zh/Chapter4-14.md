# 4.14 4G模块 测试

MYD-Y6ULX开发板提供一个支持4G模块的插槽，此插槽使用USB数据线与4G模块通讯。当前仅支持移远EC20型号。

注意：移远EC20模块为选购配件，请向米尔科技购买。

### 硬件连接

* 安装移远EC20模块到PCI-E插槽(U12)。
* 将两头I-PEX接口的天线安装在移远EC20模块和开发板的J25位置。
* 安装SMA天线到开发板的J24位置。


系统中已经加入4G模块的驱动，启动后会自动加载相应驱动,驱动加载成功后会出现对应的/dev/ttyUSB*设备，查看：
```
#ls /dev/ttyUSB*
/dev/ttyUSB0 /dev/ttyUSB1 /dev/ttyUSB2 /dev/ttyUSB3 /dev/ttyUSB4
```
* 移植pppd。

```
#tar -zxvf ppp-2.4.5.tar.gz
#cd ppp-2.4.5
#./configure
#make CC=arm-linux-gnueabihf-gcc
```
编译后生成pppd，进入chat，make编译生成chat。把生成的pppd、pppdump、pppstatus、chat等文件拷贝到arm板/usr/sbin/目录下。

* 拨号
使用quectel-pppd.sh脚本拨号
```
#./quectel-pppd.sh  //串口设备名(比如/dev/ttyUSB3) 
```
ip-up：pppd 在获取 ip 和 dns 之后，会自动调用这个脚本文件来设置系统的 DNS。
拨号成功后就可以联网了。

 使用quectel-ppp-kill来挂断拨号，pppd必须被正常挂断，否者可能会导致你下次ppp拨号失败。
```
#./quectel-ppp-kill
```
