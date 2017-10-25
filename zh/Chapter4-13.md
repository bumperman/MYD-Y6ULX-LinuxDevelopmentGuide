# 4.13 WiFi 测试

MYD-Y6ULX开发板提供一个WiFi模块(J11)，支持Client模式。

## 硬件连接

将附带SMA接口的天线安装在开发板的J12位置。

## Client模式

Client模式是用于将WiFi模块作为客户访问设备，主动连接于路由器或其它提供无线热点的设备。

系统中已经加入WiFi模块的驱动，启动后会自动加载相应驱动。驱动加载成功后会出现对应的wlan0网络设备，使用ifconfig命令来确认。

```
#ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr a0:2c:36:60:ee:e0  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3388 errors:0 dropped:10 overruns:0 frame:0
          TX packets:37 errors:0 dropped:3 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:395459 (386.1 KiB)  TX bytes:6074 (5.9 KiB)
```

下面使用wpa_passphrase生成对应WiFi热点SSID的密码，然后由wpa_supplicant命令实现WiFi模块与WiFi热点的连接。

```
#wpa_passphrase "MYiRTech" >> wifi.conf
12345678

cat wifi.conf
# reading passphrase from stdin
network={
	ssid="MYiRTech"
	#psk="12345678"
	psk=b96d9a5de2d9480ad5f987857e20216b47a0c4bf43397825ba909438bc52aaff
}

wpa_supplicant -D wext -B -i wlan0 -c wifi.conf
Successfully initialized wpa_supplicant
rfkill: Cannot open RFKILL control device
R8188EU: Firmware Version 11, SubVersion 1, Signature 0x88e1
MAC Address = a0:2c:36:60:ee:e0
IPv6: ADDRCONF(NETDEV_UP): wlan0: link is not ready
ioctl[SIOCSIWAP]: Operation not permitted
R8188EU: INFO indicate disassoc
```

连接成功后，使用udhcpc获取IP地址后，就可以使用了。

```
#udhcpc -b -i wlan0 -R
#ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr a0:2c:36:60:ee:e0  
          inet addr:192.168.1.211  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:5577 errors:0 dropped:15 overruns:0 frame:0
          TX packets:46 errors:0 dropped:3 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:651690 (636.4 KiB)  TX bytes:7472 (7.2 KiB)

```
