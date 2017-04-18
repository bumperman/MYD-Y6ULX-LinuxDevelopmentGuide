# 5.1 安装QtCreator

QtCreator安装包是一个二进制程序，直接执行就可以完成安装。

```
$ cd $DEV_ROOT/04-Sources
$ cp /media/cdrom/03-Tools/Qt/qt-creator-opensource-linux-x86_64-4.1.0.run .
$ chmod a+x qt-creator-opensource-linux-x86_64-4.1.0.run
$ sudo ./qt-creator-opensource-linux-x86_64-4.1.0.run
```
执行安装程序后，一直点击下一步即可完成。默认安装目录在"/opt/qtcreator-4.1.0"。

安装完成后，为了让QtCreator使用Yocto的SDK工具，需要对QtCreator加入环境变量。修改"/opt/qtcreator-4.1.0/bin/qtcreator.sh"文件，在"#! /bin/sh"前加入Yocto的环境配置即可，参考如下：

```
source /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-poky-linux-gnueabi
#! /bin/sh

# Use this script if you add paths to LD_LIBRARY_PATH
# that contain libraries that conflict with the
# libraries that Qt Creator depends on.
```

使用QtCreator时，请从终端执行"qtcreator.sh"来启动QtCreator，参考如下：

```
/opt/qtcreator-4.1.0/bin/qtcreator.sh &
```
