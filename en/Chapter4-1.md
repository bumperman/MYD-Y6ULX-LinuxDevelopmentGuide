# 4.1 Test LCD

This example demonstrates the operation of the FrameBuffer of Linux, enabling color and color grid testing.You need connect the LCD to MYS6ULX board LCD interface(J3).We have two kinds LCD with touch panel, 7-inch capacitive screen is MY-TFT070CV2 and 4.3inch resistive screen is MY-TFT043RV2.

The LCD screen will display the corresponding color, the following is the terminal output information:

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


## Configure for MY-TFT070RV2 module

The Linux source of MYS-6ULX series board has alread support display and touch function.The MY-TFT070RV2 touch function through ADC type.You just enable the relative function in dts file.

The first step, edit "arch/arm/boot/dts/mys-imx6ul-14x14-evk.dts" file, modify the status property of tsc node to okay value.
```
&tsc {
     pinctrl-names = "default";
     pinctrl-0 = <&pinctrl_tsc>;
     xnur-gpio = <&gpio1 3 GPIO_ACTIVE_LOW>;
     measure-delay-time = <0xfffff>;
     pre-charge-time = <0xffff>;
     status = "okay";
};
```
The second step, comment the argument of 4.3 inch screen, and enable argument of 7.0 inch screen.Search and modify the display-timings node of lcfif node, change it follow below.
```
        display-timings {
            native-mode = <&timing0>;
/*
             timing0: timing0 {
             clock-frequency = <9200000>
             hsync-len = <41>;
             vback-porch = <2>;
             vfront-porch = <4>;
             vsync-len = <10>;
 
             hsync-active = <0>;
             vsync-active = <0>;
             de-active = <1>;
             pixelclk-active = <0>;
             };
*/
             timing0: timing0 {
             clock-frequency = <33000000>;
             hactive = <800>;
             vactive = <480>;
             hfront-porch = <210>;
             hback-porch = <46>;
             hsync-len = <1>;
             vback-porch = <22>;
             vfront-porch = <23>;
             vsync-len = <20>;
 
             hsync-active = <0>;
             vsync-active = <0>;
             de-active = <1>;
             pixelclk-active = <1>;
             };
 
        };
```

## Configure for MY-TFT070CV2 module

The touch function of MY-TFT070CV2 module use I2C type.The slave device has already added to i2c2 controller node.You just disable tsc controller and enable argument of 7 inch screen.

* MYS-6ULX-IND
The first step, edit "arch/arm/boot/dts/mys-imx6ul-14x14-evk.dts" file, modify the status property of tsc node is disabled value.
```
&tsc {
     pinctrl-names = "default";
     pinctrl-0 = <&pinctrl_tsc>;
     xnur-gpio = <&gpio1 3 GPIO_ACTIVE_LOW>;
     measure-delay-time = <0xfffff>;
     pre-charge-time = <0xffff>;
     status = "disabled";
};
```
The second step, comment the argument of 4.3 inch screen.And enable the argument of 7.0 inch screen.Search and modify display-timings node of lcdif node, change it follow below.
```
        display-timings {
            native-mode = <&timing0>;
/*
             timing0: timing0 {
             clock-frequency = <9200000>
             hsync-len = <41>;
             vback-porch = <2>;
             vfront-porch = <4>;
             vsync-len = <10>;
 
             hsync-active = <0>;
             vsync-active = <0>;
             de-active = <1>;
             pixelclk-active = <0>;
             };
*/
             timing0: timing0 {
             clock-frequency = <33000000>;
             hactive = <800>;
             vactive = <480>;
             hfront-porch = <210>;
             hback-porch = <46>;
             hsync-len = <1>;
             vback-porch = <22>;
             vfront-porch = <23>;
             vsync-len = <20>;
 
             hsync-active = <0>;
             vsync-active = <0>;
             de-active = <1>;
             pixelclk-active = <1>;
             };
 
        };
```

