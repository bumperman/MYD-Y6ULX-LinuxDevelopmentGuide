# 4.11 Camera 测试

注意：本次测试需要在MYS-6ULX-IOT或MYS-6ULX-IND上安装MYB-6ULX扩展板和MY-CAM011B，同时使用支持MYB-6ULX的dtb文件启动Linux系统

MYB-6ULX扩展板上提供一个并行Camera接口(J10)，可以连接MY-CAM011B型号的Camera模块，模块之间使用FPC线连接。由于信号序列影响，请勿直接将其它型号的Camera的模块插入，否则会引起模块或开发板的损坏。

本例程演示使用一款开源的视频流软件uvc_stream，可以将Camera设备捕捉的数据显示在web页面。

## 硬件连接

使用FPC数据线将MYB-CAM011B模块和MYB-6ULX板上的J10接口相连接。

## 软件操作

uvc_stream是通过的网络传输数据，需要先设置好MYS-6ULX板的以太网IP地址，对应系统中的eth1设备。Linux系统中的MY-CAM011B模块的设备，可通通过v4l2-ctl命令来查询到，输出信息的i.MX6S_CSI表示Camera控制器，对应设备是/dev/video1。uvc_stream参数中'-y'是使用yuyv方式，'-P'后面是设置web界面的登录密码，用户名默认为uvc_user。'-r'是指定分辨率，当前仅支持800x600。可以用ctrl + c来停止。


```
ifconfig eth1 192.168.1.42
v4l2-ctl --list-devices
i.MX6S_CSI (platform:21c4000.csi):
    /dev/video1

    pxp (pxp_v4l2):
        /dev/video0

./uvc_stream -d /dev/video1 -y -P 123456 -r 800x600
```

uvc_stream提供两种web功能，snapshot和streaming。snapshot的请求URL是snapshot.jpeg，streaming的请求URL是stream.mjpeg。
PC和开发板在同一网络内时，打开流览器，输入地址[http://192.168.1.42:8080/stream.mjpeg](http://192.168.1.42:8080/stream.mjpeg)，可以看到有登录框，输入用户名为uvc_user，密码为123456，就可以看到从MY-CAM011B实时采集到的图像了。

