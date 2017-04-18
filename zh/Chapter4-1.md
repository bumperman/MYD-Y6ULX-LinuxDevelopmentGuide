# 4.1 LCD测试

本例演示对Linux FrameBuffer操作，实现颜色和彩色栅格测试。执行程序后，LCD液晶屏会出现相应颜色,以下是终端输出信息:

```
# modeset
# ./lcdtest_test 
The framebuffer device was opened successfully.
vinfo.xres=800
vinfo.yres=480
vinfo.bits_per_bits=24
vinfo.xoffset=0
vinfo.yoffset=0
red.offset=16
green.offset=8
blue.offset=0
transp.offset=0
finfo.line_length=2400
finfo.type = PACKED_PIXELS
The framebuffer device was mapped to memory successfully.
color: red   rgb_val: 00FF0000
color: green   rgb_val: 0000FF00
color: blue   rgb_val: 000000FF
color: r & g   rgb_val: 00FFFF00
color: g & b   rgb_val: 0000FFFF
color: r & b   rgb_val: 00FF00FF
color: white   rgb_val: 00FFFFFF
color: black   rgb_val: 00000000

```
