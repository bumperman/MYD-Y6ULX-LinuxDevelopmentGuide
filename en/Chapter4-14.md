# 4.14 4G LTE module Test

The MYD-Y6ULX board support LTE module through PCI-E slot with USB data line.Currently, the MYD-Y6ULX boards only support EC20 model from Quectl.

Attention: The module not default accessory part.You need buy it from MYiR.

## Hardware

* Use I-PEX interface wire connect LTE module and J25 position of board.
* Install SMA wireless antenna to J24 position.

## Software

Our Linux prebuilt system has added driver of 4G module.It will be auto loaded when system startup.
And also use ls to confirm it.

```
# ls /dev/ttyUSB*
/dev/ttyUSB0 /dev/ttyUSB1 /dev/ttyUSB2 /dev/ttyUSB3 /dev/ttyUSB4
```
* pppd porting 

```
# tar -zxvf ppp-2.4.5.tar.gz
# cd ppp-2.4.5
# ./configure
# make CC=arm-linux-gnueabihf-gcc
# cd chat
# make CC=arm-linux-gnueabihf-gcc
```

After compilation is complete,copy the executable program pppd、pppdump、pppstatus、chat to the development board.

* dial-up connection

Use the quectel-pppd.sh script to dial.

```
# ./quectel-pppd.sh // device name (/dev/ttyUSB3)
```

Get ip and dns, set the system DNS.
Dial success,you can access the Internet.

* Disconnect dialing

You must use quectel-ppp-kill to disconnect the dialing, otherwise it may go wrong.

```
# ./quectel-ppp-kill
```

