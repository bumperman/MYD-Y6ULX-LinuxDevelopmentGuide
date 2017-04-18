# 4.1 Test LCD

This example demonstrates the operation of the FrameBuffer of Linux, enabling color and color grid testing.The LCD screen will display the corresponding color, the following is the terminal output information:

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
