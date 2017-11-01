# 4.14 4G模块 测试

MYD-Y6ULX开发板提供一个支持4G模块的PCI-E插槽，此插槽使用USB数据线与4G模块通讯。当前仅支持移远EC20型号。

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
系统中已加入ppp软件包，可以直接使用。启用ppp0后会自动拨号，连接成功后即获得IP地址，D25灯常亮。还需要检查/etc/resolve.conf文件中的DNS是否设置正常。

```
# ifup ppp0
# ifconfig ppp0
ppp0      Link encap:Point-to-Point Protocol
          inet addr:10.163.130.65  P-t-P:10.64.64.64  Mask:255.255.255.255
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1500  Metric:1
          RX packets:5 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:3
          RX bytes:62 (62.0 B)  TX bytes:86 (86.0 B)

# cat /etc/resolv.conf
nameserver 202.96.128.86
nameserver 202.96.134.133
```

然后使用ping命令测试连接4G网络是否正常。
```
# ping myir-tech.com
PING s-26427.gotocdn.com (118.123.18.103) 56(84) bytes of data.
64 bytes from 118.123.18.103: icmp_seq=1 ttl=117 time=80.5 ms
64 bytes from 118.123.18.103: icmp_seq=2 ttl=117 time=179 ms
64 bytes from 118.123.18.103: icmp_seq=3 ttl=117 time=378 ms
64 bytes from 118.123.18.103: icmp_seq=4 ttl=117 time=118 ms
64 bytes from 118.123.18.103: icmp_seq=5 ttl=117 time=122 ms
64 bytes from 118.123.18.103: icmp_seq=6 ttl=117 time=177 ms
```

如果上面验证步骤有异常，可以查看日志来确定问题原因。
```
# cat /var/log/quectel-dial.log
```
