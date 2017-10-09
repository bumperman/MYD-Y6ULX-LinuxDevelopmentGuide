# 4.12 WiFi Test


The MYS-6ULX-IOT board has a WiFi module (J11)  on back.It's supports Client and AP mode.

## Hardware Connective

Use I-PEX interface of wireless antenna connect with J11 position of board.

## Client Mode

The Client mode means WiFi module as client device connect to your route or other AccessPoint device.

Our Linux prebuilt system has added driver of WiFi module.It will be auto loaded when system startup.
And also use lsmod to confirm it.The wlan0 network device has exist when driver loaded success.The ifconfig command can be used confirm it.

```
#ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr a0:2c:36:60:ee:e0  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3388 errors:0 dropped:10 overruns:0 frame:0
          TX packets:37 errors:0 dropped:3 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:395459 (386.1 KiB)  TX bytes:6074 (5.9 KiB)
```

Uses wpa_passphrase to generate password and ssid through you inputed arguments.
And use wpa_supplicant command to connect WiFi module with AccessPoint.

```
#wpa_passphrase "MYiRTech" >> wifi.conf
12345678

#cat wifi.conf
# reading passphrase from stdin
network={
	ssid="MYiRTech"
	#psk="12345678"
	psk=b96d9a5de2d9480ad5f987857e20216b47a0c4bf43397825ba909438bc52aaff
}

#wpa_supplicant -D wext -B -i wlan0 -c wifi.conf
Successfully initialized wpa_supplicant
rfkill: Cannot open RFKILL control device
R8188EU: Firmware Version 11, SubVersion 1, Signature 0x88e1
MAC Address = a0:2c:36:60:ee:e0
IPv6: ADDRCONF(NETDEV_UP): wlan0: link is not ready
ioctl[SIOCSIWAP]: Operation not permitted
R8188EU: INFO indicate disassoc
```

After the WiFi module connected with AccessPoint, it needs udhcpc service to fetch an AIP address from AccessPoint.

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

## AP Mode

AccessPoint mode needs software and hardware to suporrt AP feature. The WiFi module of MYS-6ULX-IOT  hs support AP mode.It use Hostapd to support AP function.

### Compile Hostapd

MYD-Y6ULX resource package has contains hostapd source.And prebuilt image has support hostapd package.

```
tar xvf RTL8188-hostapd-2.0.tar.gz
cd RTL8188-hostapd-2.0/hostapd
make
mkdir ~/hostapd-armhf
make install DESTDIR=~/hostapd-armhf
```

Now, the hostapd be installed in path "~/hostapd-armhf".You can throught NFS or sdcard to copy those file to your board.After that, you need uses "-v" argument for hostapd to confirm version.

```
#hostapd -v
hostapd v0.8.x_rtw_r7475.20130812_beta
User space daemon for IEEE 802.11 AP management,
IEEE 802.1X/WPA/WPA2/EAP/RADIUS Authenticator
Copyright (c) 2002-2011, Jouni Malinen <j@w1.fi> and contributors
```

The configure file of hostapd is "/etc/hostapd/hostapd.conf". It used for configure SSID and passcode of WiFi network.The "ssid" option is name of WiFi.The "pass_passphrase" option is passcode of WiFi network.
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

Running hostapd as daemon type:
```
ifconfig wlan0 up
hostapd /etc/hostapd/hostapd.conf -B
```

The hostapd only support AP function.We also need DHCP service to distribute IP address for each client device of connected to WiFi network.
The udhcpd command implement a simple DHCP server fun server function.

Firstly, write below codes to /etc/udhcpd.conf file. If file not exist, please create it.

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

Secondly, setting wlan0 as route IP address, and running udhcpd service.
```
ifconfig wlan0 192.168.2.1
udhcpd -fS /etc/udhcpd.conf
```
Now, you can use mobile or other WiFi device to connect "myir-test" WiFi signal.Also, the device will get an IP address.
