# 6 系统更新

MYS-6ULx系列板的系统更新使用两种方法，MfgTool更新和SD卡更新。

## 安装工具

烧写工具是由NXP公司提供的MfgTool 2.7.0版本，光盘中路径"03-Tools\MfgTool"目录下，支持Windows和Linux操作系统。解压后的目录中有多个vbs文件，这些是配置好的烧写脚本。执行后即可启动MfgTool程序。

## MfgTool更新系统

更新具体步骤如下(顺序不可颠倒):

* 拨动启动拨码开关(SW1)的第3位为ON，第4位为OFF。
* 连接开发板电源(J1)。
* 使用mini-USB线连接PC机USB端口与开发板
* 双击MfgTool目录下的"mfgtool2-yocto-mx6ul-evk-nand.vbs"文件，此时可以看到MfgTool界面已识别到开发板。
* 点击MfgTool界面上的"Start"按钮，MfgTool就开始自动更新系统至板载存储设备。

更新系统前也可以连接开发板串口(JP1)，以便查看更新过程或分析失败原因。

## SD卡更新系统

使用HP Format工具格式化MicroSD卡，把"02-Images\SD-update"目录下的所有文件拷贝到MicroSD存储卡。

