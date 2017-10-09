# 4.13 WiFi 测试


MYD-Y6ULX开发板提供一个WiFi模块(J11)，支持Client和AP模式，本节分别测试两种场景下的使用方法。

## 硬件连接

将附带I-PEX接口的天线安装在开发板的J12位置。

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

## AP模式

AP模式是由软件和硬件同时支持才可以实现，MYD-Y6ULX板上的WiFi模块可以支持AP模式。软件上使用Hostapd来实现热点配置功能。

### 编译Hostapd

资源包中有提供hostapd的源码，同时提供的镜像中也有安装hostapd软件。

```
#tar xvf RTL8188-hostapd-2.0.tar.gz
#cd RTL8188-hostapd-2.0/hostapd
#make
mkdir ~/hostapd-armhf
#make install DESTDIR=~/hostapd-armhf
```

这里把hostapd安装在了"~/hostapd-armhf"位置，可以使用NFS或sdcard将其复制到开发板上。可以使用"-v"检查版本信息。

```
hostapd -v
hostapd v0.8.x_rtw_r7475.20130812_beta
User space daemon for IEEE 802.11 AP management,
IEEE 802.1X/WPA/WPA2/EAP/RADIUS Authenticator
Copyright (c) 2002-2011, Jouni Malinen <j@w1.fi> and contributors
```

## 配置Hostapd

hostapd的配置文件是"/etc/hostapd/hostapd.conf"，用于配置SSID和热点的密码。"ssid"参数是WiFi热点的名称，"pass_passphrase"是WiFi热点的密码。
```
#cat /etc/hostapd/hostapd.conf 
# Basic configuration

interface=wlan0
ssid=myir-test
channel=1
#bridge=br0

# WPA and WPA2 configuration

macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=12345678
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP

# Hardware configuration

driver=rtl871xdrv
ieee80211n=1
hw_mode=g
device_name=RTL8192CU
manufacturer=Realtek
```

Hostapd以daemon方式运行，命令如下：
```
#ifconfig wlan0 up
#hostapd /etc/hostapd/hostapd.conf -B
```

Hostapd只是提供AP的功能，还需要有DHCP服务才可以给连接到WiFi网络的设备分配IP地址。udhcpd命令实现了简单的DHCP服务器功能。首先将下面的配置写入/etc/udhcpd.conf文件，若没有请先创建该文件。

```
# The start and end of the IP lease block
start 		192.168.2.20	#default: 192.168.0.20
end		192.168.2.254	#default: 192.168.0.254

# The interface that udhcpd will use
interface	wlan0		#default: eth0

# The maximim number of leases (includes addressesd reserved
# by OFFER's, DECLINE's, and ARP conficts

#max_leases	254		#default: 254


# If remaining is true (default), udhcpd will store the time
# remaining for each lease in the udhcpd leases file. This is
# for embedded systems that cannot keep time between reboots.
# If you set remaining to no, the absolute time that the lease
# expires at will be stored in the dhcpd.leases file.

#remaining	yes		#default: yes


# The time period at which udhcpd will write out a dhcpd.leases
# file. If this is 0, udhcpd will never automatically write a
# lease file. (specified in seconds)

#auto_time	7200		#default: 7200 (2 hours)


# The amount of time that an IP will be reserved (leased) for if a 
# DHCP decline message is received (seconds).

#decline_time	3600		#default: 3600 (1 hour)


# The amount of time that an IP will be reserved (leased) for if an
# ARP conflct occurs. (seconds

#conflict_time	3600		#default: 3600 (1 hour)


# How long an offered address is reserved (leased) in seconds

#offer_time	60		#default: 60 (1 minute)

# If a lease to be given is below this value, the full lease time is
# instead used (seconds).

#min_lease	60		#defult: 60


# The location of the leases file

#lease_file	/var/lib/misc/udhcpd.leases	#defualt: /var/lib/misc/udhcpd.leases

# The location of the pid file
#pidfile	/var/run/udhcpd.pid	#default: /var/run/udhcpd.pid

# Everytime udhcpd writes a leases file, the below script will be called.
# Useful for writing the lease file to flash every few hours.

#notify_file				#default: (no script)

#notify_file	dumpleases 	# <--- usefull for debugging

# The following are bootp specific options, setable by udhcpd.

#siaddr		192.168.0.22		#default: 0.0.0.0

#sname		zorak			#default: (none)

#boot_file	/var/nfs_root		#default: (none)

# The remainer of options are DHCP options and can be specifed with the
# keyword 'opt' or 'option'. If an option can take multiple items, such
# as the dns option, they can be listed on the same line, or multiple
# lines. The only option with a default is 'lease'.

#Examles
opt	dns	192.168.2.1
option	subnet	255.255.255.0
opt	router	192.168.2.1
#opt	wins	192.168.10.10
#option	dns	129.219.13.81	# appened to above DNS servers for a total of 3
option	domain	local
option	lease	864000		# 10 days of seconds

```

然后将wlan0作为路由，运行udhcpd服务：
```
#ifconfig wlan0 192.168.2.1
#udhcpd -fS /etc/udhcpd.conf
```
使用手机或其他WiFi设备连接"myir-test"热点后，即可分配到正确的IP地址。
