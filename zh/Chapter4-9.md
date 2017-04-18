# 4.9 Audio 测试

本例程演示使用Linux系统中的arecord/aplay命令对音频接口录音和放音。需要使用两头3.5mm的音频AUX线，从电脑音频输出孔和开发板的LINE IN(J16)接口连接，HEADERPHONE(J14)连接音箱。拷贝并运行程序Audio，电脑播放音频文件，这里音箱中会播放从电脑输入的音频。

```
arecord -f dat -t wav test.wav
aplay -f dat test.wav
```
