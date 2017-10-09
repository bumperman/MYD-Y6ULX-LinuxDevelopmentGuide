# 4.9 RS232 测试

本例程演示如何使用 Linux Serial API编程，使用RS232接口，实现数据发送和接收，详细请参考源码。

## 硬件连接
MYD-Y6ULX上有一个RS232接口(J10)，可以将TXD，RXD信号线与另外的RS232设备相连接。或者是USB转RS232的转换器设备,此处转接到USB设备连接到PC端。

## 软件测试

将编译出来的可执行程序拷贝至MYD-Y6ULX开发板系统内。MYD-Y6ULX作为发送端执行以下命令，PC端接收数据。

```
./uart_test -d /dev/ttymxc1 -b 115200
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
/dev/ttyS1 RECV 10 total
/dev/ttyS1 RECV: 1234567890
```
在PC端可以使用串口工具查看接收的数据。

