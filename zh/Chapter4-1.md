# 4.1 LCD测试

本例程演示对Linux的FrameBuffer设备操作，实现液晶输出显示RGB颜色和颜色合成测试。例程基于Linux FrameBuffer API接口开发。测试前需要把LCD连接至J8接口上。米尔科技提供两种LCD模块，分别是7寸的MY-TFT070CV2和4.3寸的MY-TFT043RV2。提供的prebuilt镜像是默认为4.3寸液晶的。

执行程序后，LCD液晶屏会出现相应颜色,以下是终端输出信息:

```
./framebuffer_test
The framebuffer device was opened successfully.
vinfo.xres=480
vinfo.yres=272
vinfo.bits_per_bits=16
vinfo.xoffset=0
vinfo.yoffset=0
red.offset=11
green.offset=5
blue.offset=0
transp.offset=0
finfo.line_length=960
finfo.type = PACKED_PIXELS
The framebuffer device was mapped to memory successfully.
color: red   rgb_val: 0000F800
color: green   rgb_val: 000007E0
color: blue   rgb_val: 0000001F
color: r & g   rgb_val: 0000FFE0
color: g & b   rgb_val: 000007FF
color: r & b   rgb_val: 0000F81F
color: white   rgb_val: 0000FFFF
color: black   rgb_val: 00000000
```
