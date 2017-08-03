# 4.11 Test Camera

Attention: This example needs install the MYB-6ULX on MYS-6ULX-IOT or MYS-6ULX-IND.And uses dtb file to boot Linux that supoorts MYB-6ULX board.

MYB-6ULX board has an paraller camera interface(J10).It can connects camera module of MY-CAM011B model.The module and board connects with FPC wire.Inorder the signal wire order, please do not insert other Camera module  into interface.This operation will damage your board or camera module.

This example program use an open source software uvc_stream.It supports show video in web from camera capture.

## Hardware connect

Use FPC wire connects MYB-CAM011B module and camera interface J10 of MYB-6ULX.

## Software operations

The uvc_stream through network show video data.You need setup ethernet IP address of MYS-6ULX, the correspond device is eth1. The MY-CAM011B module device node is /dev/video1 in Linux system. The uvc_stream parameter '-y' means use yuyv type, the '-P' means setting password of web page. The uvc_stream default username is uvc_user.
```
ifconfig eth1 192.168.1.42
./uvc_stream -d /dev/video1 -y -P 123456
```

The uvc_stream program supports two kinds web functions, snapshot and streaming. The snapshot function request URL is snapshot.jpeg, and streaming function request URL is stream.mjpeg.

Let PC and board has same network, open your browser, visit [http://192.168.1.42:8080/stream.mjpeg](http://192.168.1.42:8080/stream.mjpeg).After enter, you can see the login window, login with uvc_user, 123456.Now, you can see video stream from web on MY-CAM011B captured.

