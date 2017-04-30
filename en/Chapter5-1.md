# 5.1 Install QtCreator

QtCreator installation package is a binary program, can be directly to install to your host PC.

```
$ cd $DEV_ROOT/04-Sources
$ cp /media/cdrom/03-Tools/Qt/qt-creator-opensource-linux-x86_64-4.1.0.run .
$ chmod a+x qt-creator-opensource-linux-x86_64-4.1.0.run
$ sudo ./qt-creator-opensource-linux-x86_64-4.1.0.run
```
When the installation process is done, click on the next step to complete. The default installation directory is in the "/opt/qtcreator-4.1.0".

Inorder to QtCreator use Yocto SDK, we need add environment to QtCreator, modify the file "/opt/qtcreator-4.1.0/bin/qtcreator.sh". Add below command before the line "#! /bin/sh":

```
vi /opt/qtcreator-4.1.0/bin/qtcreator.sh
source /opt/myir-imx6ulx-fb/4.1.15-2.0.1/environment-setup-cortexa7hf-neon-poky-linux-gnueabi
#! /bin/sh

# Use this script if you add paths to LD_LIBRARY_PATH
# that contain libraries that conflict with the
# libraries that Qt Creator depends on.
```

When you use QtCreator, you need start it from terminal to execute "qtcreator.sh".

```
/opt/qtcreator-4.1.0/bin/qtcreator.sh &
```
