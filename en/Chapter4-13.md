# 4.13 Test WiFi

Attention: The WiFi of carrier board only for NAND version of board.

The MYD-Y6ULX board has a WiFi module (J11).It's supports Client mode.

## Hardware Connective

Use SMA interface of wireless antenna connect with J11 position of board.

## Client Mode

The Client mode means WiFi module as client device connect to your route or other AccessPoint device.

Our Linux prebuilt system has added driver of WiFi module.It will be auto loaded when system startup.
And also use lsmod to confirm it.The wlan0 network device has exist when driver loaded success.The ifconfig command can be used confirm it.

```
# ifconfig wlan0
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
# wpa_passphrase "MYiRTech" >> wifi.conf
12345678

# cat wifi.conf
network={
	ssid="MYiRTech"
	#psk="12345678"
	psk=b96d9a5de2d9480ad5f987857e20216b47a0c4bf43397825ba909438bc52aaff
}

# wpa_supplicant -D wext -B -i wlan0 -c wifi.conf
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
# udhcpc -b -i wlan0 -R
# ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr a0:2c:36:60:ee:e0  
          inet addr:192.168.1.211  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:5577 errors:0 dropped:15 overruns:0 frame:0
          TX packets:46 errors:0 dropped:3 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:651690 (636.4 KiB)  TX bytes:7472 (7.2 KiB)

```
