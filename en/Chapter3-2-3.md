# CAN配置

通过CAN控制器can0、can1寻找dts文件中的有关配置并修改status = "okay" 使能can:

```
can0: can@f000c000 {
                   compatible = "atmel,at91sam9x5-can";
                   reg = <0xf000c000 0x300>;
                   interrupts = <40 IRQ_TYPE_LEVEL_HIGH 3>;
                   pinctrl-names = "default";
                   pinctrl-0 = <&pinctrl_can0_rx_tx>;
                   clocks = <&can0_clk>;
                   clock-names = "can_clk";
                   status = "okay";
                   };

can1: can@f8010000 {
                   compatible = "atmel,at91sam9x5-can";
                   reg = <0xf8010000 0x300>;
                   interrupts = <41 IRQ_TYPE_LEVEL_HIGH 3>;
                   pinctrl-names = "default";
                   pinctrl-0 = <&pinctrl_can1_rx_tx>;
                   clocks = <&can1_clk>;
                   clock-names = "can_clk";
                   status = "okay";
                   };
```

