# 4.12 Test Camera

MYD-Y6ULX board has an paraller camera interface(J9).It can connects camera module of MY-CAM011B model.The module and board connects with FPC wire.Inorder the signal wire order, please do not insert other Camera module  into interface.This operation will damage your board or camera module.

This example program use an open source software uvc_stream.It supports show video in web from camera capture.

## Hardware connect

Use FPC wire connects MYB-CAM011B module and camera interface J9 of MYD-Y6ULX.

## Software operations

The uvc_stream through network show video data.You need setup ethernet IP address of MYD-Y6ULX, the correspond device is eth1. Uses "v4l2-ctl" command to query the device node of MY-CAM011B on Linux system.It outputs information about video device.The "i.MX6S_CSI" string is camera controller and correspond string "/dev/video1" is device node of MY-CAM011B module. The uvc_stream parameter '-y' means use yuyv type, the '-P' means setting password of web page. The '-r' means define resolution, the camera only support 800x600.The uvc_stream default username is uvc_user.
```
# ifconfig eth1 192.168.1.42
# v4l2-ctl --list-devices
 
    i.MX6S_CSI (platform:21c4000.csi):
    /dev/video1

    pxp (pxp_v4l2):
        /dev/video0

# ./uvc_stream -d /dev/video1 -y -P 123456
```

The uvc_stream program supports two kinds web functions, snapshot and streaming. The snapshot function request URL is snapshot.jpeg, and streaming function request URL is stream.mjpeg.

Let PC and board has same network, open your browser, visit [http://192.168.1.42:8080/stream.mjpeg](http://192.168.1.42:8080/stream.mjpeg).After enter, you can see the login window, login with uvc_user, 123456.Now, you can see video stream from web on MY-CAM011B captured.

