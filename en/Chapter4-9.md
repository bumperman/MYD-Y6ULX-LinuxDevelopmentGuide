# 4.9 Test RS232

This example demonstrates how to use the Linux serial API to configure the RS232 on the development board to send and receive data. For details, refer to the source code.


## Hardware
MYD-Y6ULX board have a RS232 interface(J10.9 for RS232-TX, J10.10 for RS232-RX).You need connect the TXD,RXD signal wire to another RS232 device or USB to RS232 converter.

## Software

Copy and run the program on MYD-Y6ULX Linux system.Below is MYD-Y6ULX as the sender:

```
# ./uart_test -d /dev/ttymxc1 -b 115200
/dev/ttymxc1 RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
/dev/ttymxc1  RECV 10 total
/dev/ttymxc1  RECV: 1234567890
```

