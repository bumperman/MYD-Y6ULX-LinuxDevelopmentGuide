# 4.1 LCD测试

本例程演示对Linux的FrameBuffer设备操作，实现液晶输出显示RGB颜色和颜色合成测试。例程基于Linux FrameBuffer API接口开发。测试前需要把LCD连接至J8接口上。米尔科技提供两种LCD模块，分别是7寸的MY-TFT070CV2和4.3寸的MY-TFT043RV2。提供的prebuilt镜像是默认为4.3寸液晶的。

执行程序后，LCD液晶屏会出现相应颜色,以下是终端输出信息:

```
# ./framebuffer_test
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

## 支持MY-TFT070RV2的配置方法

MYS-6ULX开发板中提供的Linux代码已经支持该模块的显示和触摸功能。MY-TFT070RV2的触摸功能是通过ADC采样方式，dts代码中已配置好,只需要启用相应功能即要可。

* MYS-6ULX-IND  
  第一步，编辑"arch/arm/boot/dts/mys-imx6ul-14x14-evk.dts"文件，修改tsc的status属性为okay。

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

  第二步，将默认的4.3寸屏莫的配置注释，并打开7.0寸的配置。找到lcfif节点下的display-timings节点，修改如下：

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

* MYS-6ULX-IoT  
  MYS-6ULX-IoT的修改方法和MYS-6ULX-IND的相同，编辑的文件为"arch/arm/boot/dts/mys-imx6ull-14x14-evk.dts"。

## 支持MY-TFT070CV2的配置方法

MY-TFT070CV2模块的触摸使用的是I2C方式通讯，丛设备已添加到i2c2控制器上。使用前禁用tsc控制器，再启用7寸屏的配置参数即可。

* MYS-6ULX-IND  
  第一步，编辑"arch/arm/boot/dts/mys-imx6ul-14x14-evk.dts"文件，修改tsc的status属性为disabled。

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

  第二步，将默认的4.3寸屏莫的配置注释，并打开7.0寸的配置。找到lcfif节点下的display-timings节点，修改如下：

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

* MYS-6ULX-IoT  
  MYS-6ULX-IoT的修改方法和MYS-6ULX-IND的相同，编辑的文件为"arch/arm/boot/dts/mys-imx6ull-14x14-evk.dts"。



