# 4.10 Audio 测试

注意：本例程需要在MYS-6ULX-IOT或MYS-6ULX-IND上安装MYB-6ULX扩展板，同时使用支持MYB-6ULX的dtb文件启动Linux系统

## 硬件连接

本例程演示使用Linux系统中的arecord/aplay命令对音频接口录音和放音。需要使用两头3.5mm的音频AUX线，从电脑音频输出孔和开发板的LINE IN(J7)接口连接，HEADERPHONE(J5)连接耳机。

## 软件操作

在电脑中播放音频文件，执行arecord命令会先将LINE IN中的音频录制并保存为test.wav文件。运行一分钟后再按ctrl + c来停止。
```
arecord -f cd test.wav
```

执行aplay命令来播放上面录制好的音频文件。
```
aplay test.wav
```

