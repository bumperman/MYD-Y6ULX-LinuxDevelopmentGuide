# 4.4 GPIO-KEY 测试

本例演示如何在Linux用户空间读取按键状态和键值。运行gpio_key程序后，按下或释放S2按键，串口会输出相应按键的状态信息。按下"Ctrl-C"可退出程序。

在开发板的控制终端上执行程序:

```
# ./gpio_key /dev/input/event2
Hit any key on board ......
key 2 Pressed
key 2 Released
key 2 Pressed
key 2 Released
```

