# 3.3.3 Yocto常见问题


## Q1:Yocto构建时出现U-Boot编译问题

编译错误信息如下：

```
WARNING: u-boot-mys6ulx-2016.03-r0 do_fetch: Failed to fetch URL git:////home/KevinChen/MYiR-iMX-uboot;protocol=file;branch=mys-6ulx, attempting MIRRORS if available
ERROR: u-boot-mys6ulx-2016.03-r0 do_fetch: Fetcher failure: Unable to find revision 38cc50da55a891ba0ac09346f3a7a6cbb4a20970 in branch mys-6ulx even from upstream
ERROR: u-boot-mys6ulx-2016.03-r0 do_fetch: Function failed: Fetcher failure for URL: 'git:////home/KevinChen/MYiR-iMX-uboot;protocol=file;branch=mys-6ulx'. Unable to fetch URL from any source.
ERROR: Logfile of failure stored in: /home/KevinChen/MYD-Y6ULX-devel/fsl-release-yocto/myd-y6uly2/tmp/work/myd_y6ull14x14-poky-linux-gnueabi/u-boot-mys6ulx/2016.03-r0/temp/log.do_fetch.4991
ERROR: Task 206 (/home/KevinChen/MYD-Y6ULX-devel/fsl-release-yocto/sources/meta-myir-imx6ulx/recipes-bsp/u-boot/u-boot-mys6ulx_2016.03.bb, do_fetch) failed with exit code '1'
NOTE: Tasks Summary: Attempted 3116 tasks of which 3115 didn't need to be rerun and 1 failed.
No currently running tasks (1771 of 3136)

Summary: 1 task failed:
  /home/KevinChen/MYD-Y6ULX-devel/fsl-release-yocto/sources/meta-myir-imx6ulx/recipes-bsp/u-boot/u-boot-mys6ulx_2016.03.bb, do_fetch
Summary: There were 3 WARNING messages shown.
Summary: There were 2 ERROR messages shown, returning a non-zero exit code.
```

出现这种情况是由于U-Boot更新后，Yocto没有更新的对应的版本。
修改步骤如下：

1. 进入U-Boot源码目录，使用"git log"查看commit id并复制
2. 修改Yocto源码目录下的"source/meta-myir-imx6ulx/recipes-bsp/u-boot/u-boot-mys6ulx_2016.03.bb"文件中的SRCREV变量为commit id即可。

## Q2:Yocto构建时出现Linux kernel编译问题

此问题和上一个问题相似，同样是Linux Kernel更新后，Yocto没有更新版本。修改步骤如下：

1. 进入Linux源码目录，使用"git log"查看commit id并复制
2. 修改Yocto源码目录下的"source/meta-myir-imx6ulx/recipes-kernel/linux/linux-mys6ulx_4.1.15.bb"文件中的SRCREV变量为commit id即可。

## Q3:如何重新加载己存在的构建目录

第一次构建时，使用以下命令来创建一个构建目录build，创建完成后会在build目录下。

```
DISTRO=myir-imx-fb MACHINE=myd-y6ull14x14 source fsl-setup-release.sh -b build
```

Yocto中途退出或中断后，可以重新打开新的shell终端，重新加载build构建目录，命令如下：

```
source fsl-setup-release.sh build
```