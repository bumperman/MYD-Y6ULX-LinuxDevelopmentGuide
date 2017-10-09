# 4.8 Test RS485

This example demonstrates how to use the Linux serial API to configure the RS485 on the development board to send and receive data. For details, refer to the source code.


## Hardware
MYD-Y6ULX board have an RS485 interface(J10).You need connect the TXD,RXD signal wire to another RS232 device or USB to RS485 converter.

## Software

Copy and run the program on MYD-Y6ULX Linux system.Below is MYD-Y6ULX as the sender:

```
./uart_test -d /dev/ttymxc1 -b 115200
/dev/ttymxc1 RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
```

