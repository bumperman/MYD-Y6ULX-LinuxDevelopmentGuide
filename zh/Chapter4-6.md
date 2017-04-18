# 4.6 Ethernet 测试

本例使用 TCP/IP sokect API，实现一个简单的C/S结构的程序。将可执行程序arm_client拷贝至开发板，pc_server拷贝至PC，将开发板和PC接入网络。

在 PC 上配置IP并运行服务程序:

```
sudo ifconfig eth0 192.168.1.111
./pc_server
REC FROM: 192.168.1.222
```

在开发板上运行客户程序，将看到所发送的信息:

```
ifconfig eth0 192.168.1.222
./arm_client 192.168.1.111
form server: Make Your idea Real!
```
