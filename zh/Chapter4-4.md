# 4.4 RS232 测试

本例程演示使用Linux API配置开发板上的RS232串口(J11)并使其发送和接收数据。将开发板RS232(J11)与PC机的DB9串口连接，并将PC串口的波特率设为 115200，数据位为8，停止位为1，无奇偶校验。将可执行程序uart_test拷贝至开发板并执行以下命令，PC串口终端打印如下信息:

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
