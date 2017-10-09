# 4.10 CAN Bus 测试

本例程演示使用Linux socket CAN API，使用MYD-Y6ULX上的CAN总线接口发送和接收数据。将can_send和can_receive拷贝至开发板。执行以下步骤:

## 硬件连接
MYD-Y6ULX开发板有一个CAN总线接口(J10)，将H，L信号线与另外的CAN通讯设备或USB CAN转换器相连接。

## 软件测试
配置开发板上CAN0通信波特率都设置为 50kbps，并使能CAN0设备

Linux上可以使用两种工具来配置CAN设备，canconfig和ip，MYD-Y6ULX附带的系统默认使用ip命令。
canconfig命令配置：
```
canconfig can0 bitrate 50000 ctrlmode triple-sampling on
canconfig can0 start
```
ip命令配置
```
ip link set can0 type can bitrate 50000 triple-sampling on
ifconfig can0 up
```

CAN收发测试可以使用系统附带的cansend、candump命令，也可以使用资源包中CAN收发例程。

- MYD-Y6ULX作为发送端：

使用cansend发送数据到CAN总线：
```
cansend can0 100#01.02.03.04.05.06.07.08
```

can_send例程运行后会一直发送数据，直到ctrl + c结束。
```
./can_send -d can0 -i 100 0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
```

- 其他设备作为接收端：

使用candump接收CAN数据：

```
candump can0
can0  100   [8]  01 02 03 04 05 06 07 08
```

can_receive例程接收来自CAN总线的数据：

```
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
```
