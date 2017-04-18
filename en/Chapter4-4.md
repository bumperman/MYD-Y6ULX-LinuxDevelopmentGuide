# 4.4 Test RS232

This example demonstrates use of the Linux API to configure the RS232(J11) port on the development board to send and receive data. The  RS232 of board connect PC DB9 serial port

Copy the uart_test file to board and run it, here is serial port output information:

```
./uart_test -d /dev/ttyS1 -b 115200 
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
```
