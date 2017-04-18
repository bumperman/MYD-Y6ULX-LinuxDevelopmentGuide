# RS485配置

通过产品硬件原理图及CPU datasheet可以得知RS485的控制器为usart2, 之后我们在dts文件中寻找usart2的有关信息并修改status = "okay"使能RS485:

```
usart2: serial@f8020000 {
                        compatible = "atmel,at91sam9260-usart";
                        reg = <0xf8020000 0x100>;
                        interrupts = <14 IRQ_TYPE_LEVEL_HIGH 5>;
                        dmas = <&dma1 2 AT91_DMA_CFG_PER_ID(7)>,
                               <&dma1 2 (AT91_DMA_CFG_PER_ID(8) | AT91_DMA_CFG_FIFOCFG_ASAP)>;
                        dma-names = "tx", "rx";
                        pinctrl-names = "default";
                        pinctrl-0 = <&pinctrl_usart2>;
                        clocks = <&usart2_clk>;
                        clock-names = "usart";
                        status = "okay";
                        };

```
