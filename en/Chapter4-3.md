# 4.3 Test RS485

This example demonstrates how to use the Linux API to configure the RS485 on the development board to send and receive data. For details, refer to the source code.
The port RS485(J13)  of board connect to other RS485 port with A, B data line.

Copy and run the program on board, below is the sender command:

```
./rs485_write -d /dev/ttyS2 -b 115200 -e 1
SEND:0123456789
SEND:0123456789
SEND:0123456789
SEND:0123456789
SEND:0123456789
SEND:0123456789
```
The reciver:

```
./rs485_read -d /dev/ttyS2 -b 115200 -e 1
RECV:0123456789, total:10
RECV:0123456789, total:10
RECV:0123456789, total:10
RECV:0123456789, total:10
RECV:0123456789, total:10
RECV:0123456789, total:10
RECV:0123456789, total:10
```
