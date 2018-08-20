# 3.3.3 Yocto Build FAQ


## Q1:U-Boot compile error when Yocto building

Below is the error message:

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

Generally, this case is cause by U-Boot update while the Yocto hasn't update with match version.

Below is the modify steps:

1. Move into U-Boot source directory.And checkout the commit id use "git log" command.
2. Modify the SRCREV variable value of "source/meta-myir-imx6ulx/recipes-bsp/u-boot/u-boot-mys6ulx_2016.03.bb"  file under the Yocto source directory with the commit id.

## Q2:Linux compile error when Yocto building

This problem same with previous one.The Linux kernel source updated while the Yocto hasn't update with match version. 

Below is the modify steps:

1. Move into Linux source directory.And checkout the commit id use "git log" command.
2. Modify the SRCREV variable value in "source/meta-myir-imx6ulx/recipes-kernel/linux/linux-mys6ulx_4.1.15.bb"  file under the Yocto source directory with the commit id .