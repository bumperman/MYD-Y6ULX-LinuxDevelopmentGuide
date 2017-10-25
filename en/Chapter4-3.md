# 4.3 Ethernet

This example uses the TCP/IP socket API to implement a simple C/S structure of the program. Copy the executable program arm_client to the development board, pc_server copy to the PC, the development board and PC access network.

The MYD-Y6ULX has two ethernet interfaces, CN1 and CN2.

Configure IP of PC machine and run server program:

```
$ sudo ifconfig eth0 192.168.1.111
$ ./pc_server
REC FROM: 192.168.1.222
```

Run client program on board:

```
# ifconfig eth0 192.168.1.222
# ./arm_client 192.168.1.111
form server: Make Your idea Real!
```
