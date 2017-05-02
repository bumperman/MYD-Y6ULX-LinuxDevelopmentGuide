# 4.2 触摸测试

MYS-6ULX支持两种触摸方式，电容和电阻。米尔科技可提供两种带触摸的液晶，7寸电容MY-TFT070CV2和4.3寸电阻MY-TFT043RV2。

触摸测试可以使用ts_calibrate和ts_test命令，ts_calibrate用于触摸校验，ts_test用于测试。其中，命令需要变量"TSLIB_TSDEVICE"来找到触摸设备，不同触摸方式的设备节点不一定相同，请对应设备填写。


```
export TSLIB_TSDEVICE=/dev/input/event1
# ts_calibrate

# ts_test

```
