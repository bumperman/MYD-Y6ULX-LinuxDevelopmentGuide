# 4.14 WiFi Test


The MYD-Y6ULX board has a 4G module.

## Hardware Connective

Use I-PEX interface of wireless antenna connect with J24 position of board.



Our Linux prebuilt system has added driver of 4G module.It will be auto loaded when system startup.
And also use ls to confirm it.
```
#ls /dev/ttyUSB*
/dev/ttyUSB0 /dev/ttyUSB1 /dev/ttyUSB2 /dev/ttyUSB3 /dev/ttyUSB4
```
* pppd porting 
```
#tar -zxvf ppp-2.4.5.tar.gz
#cd ppp-2.4.5
#./configure
#make CC=arm-linux-gnueabihf-gcc
#cd chat
#make CC=arm-linux-gnueabihf-gcc
```
After compilation is complete,copy the executable program pppd、pppdump、pppstatus、chat to the development board.

* dial-up connection
Use the quectel-pppd.sh script to dial.
```
./quectel-pppd.sh // device name (/dev/ttyUSB3)
```
Get ip and dns, set the system DNS.
Dial success,you can access the Internet.
* Disconnect dialing
You must use quectel-ppp-kill to disconnect the dialing, otherwise it may go wrong.
```
./quectel-ppp-kill
```



