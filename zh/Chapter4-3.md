# 4.6 Ethernet 测试

本例使用Linux sokect API，实现简单的C/S结构的程序，两个程序通过TCP/IP协议栈通信。将可执行程序arm\_client拷贝至开发板，pc\_server拷贝至PC，将开发板和PC接入网络。

## MYS-6ULX 网口

在 PC 上配置IP并运行服务程序:

```
# sudo ifconfig eth0 192.168.1.111
# ./pc_server
REC FROM: 192.168.1.222
```

在开发板上运行客户程序，将看到所发送的信息:

```
# ifconfig eth0 192.168.1.222
# ./arm_client 192.168.1.111
form server: Make Your idea Real!
```

## MYB-6ULX 网口

注意：本例程需要在MYS-6ULX-IOT或MYS-6ULX-IND上安装MYB-6ULX扩展板，同时使用支持MYB-6ULX的dtb文件启动Linux系统

MYS-6ULX-IOT或MYS-6ULX-IND安装MYB-6ULX扩展板后，系统中的eth0设备是MYB-6ULX网口，eth1设备是MYS-6ULX-IOT或MYS-6ULX-IND网口。

两个网口测试时，可以分别连接至两个不同网段的路由器或交换机。

测试双网口通讯，设置两个网段的IP地址，使用ping命令测试网络连通性。

```
ifconfig eth0 192.168.1.100
ifconfig eth1 192.168.2.100
ping 192.168.1.101
ping 192.168.2.101
```



