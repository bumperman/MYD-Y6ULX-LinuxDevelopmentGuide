# 4.14 Test 4G LTE

The MYD-Y6ULX board support LTE module through PCI-E slot with USB data line.Currently, the MYD-Y6ULX boards only support EC20 model from Quectl.

Attention: The module not default accessory part.You need buy it from MYiR.

## Hardware

* Install Quectl EC20 module into PCI-E slot(U12).
* Use I-PEX interface wire connect LTE module and J25 position of board.
* Install SMA wireless antenna to J24 position.

## Software

Our Linux prebuilt system has added driver of 4G module.It will be auto loaded when system startup.
And also use ls to confirm it.

```
# ls /dev/ttyUSB*
/dev/ttyUSB0 /dev/ttyUSB1 /dev/ttyUSB2 /dev/ttyUSB3 /dev/ttyUSB4
```
The Linux system of MYD-Y6ULX series board has provider ppp package.You can just enable ppp0 device, it will auto dial-up.

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

Using the ping command to test whether the module is connected to the 4G network.
```
# ping myirtech.com
PING myirtech.com (50.6.151.71) 56(84) bytes of data.
64 bytes from 118.123.18.103: icmp_seq=1 ttl=117 time=80.5 ms
64 bytes from 118.123.18.103: icmp_seq=2 ttl=117 time=179 ms
64 bytes from 118.123.18.103: icmp_seq=3 ttl=117 time=378 ms
64 bytes from 118.123.18.103: icmp_seq=4 ttl=117 time=118 ms
64 bytes from 118.123.18.103: icmp_seq=5 ttl=117 time=122 ms
64 bytes from 118.123.18.103: icmp_seq=6 ttl=117 time=177 ms
```

If you happen any issue on above steps, please check the log to find the reason.
```
# cat /var/log/quectel-dial.log
```
