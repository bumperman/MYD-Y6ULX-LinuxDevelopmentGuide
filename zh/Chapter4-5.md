# 4.8 GPIO-KEY 测试

本例程演示使用Linux系统API操作开发板上两个LED灯，D8和D9。运行程序后，D8和D9交替闪烁。按下"Ctrl-C"可结束程序。

```
# ./gpio_led /sys/class/leds/D8/brightness /sys/class/leds/D9/brightness
```

