# 4.2 RTC 测试

本例程演示使用Linux API对开发板上的RTC进行时间设置与读取。将可执行程序rtc_test拷贝至开发板。

执行程序设置当前时间:

```
# ./rtc_test -s 11 03 40 2014 08 14
date/time is updated to: 14-8-2014, 11:03:40.
```

然后读取时间:

```
# ./rtc_test
Current RTC date/time is 14-8-2014, 11:03:50.
```

