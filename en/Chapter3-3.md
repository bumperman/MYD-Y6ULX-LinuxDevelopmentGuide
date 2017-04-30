# 3.3 Build File System

The Linux platform has many open source tool to build filesystem.These tools has some features to imporve developer build filesystem more easier in system build or customize it.Recently, some are more populator Buildroot, Yocto, OpenEmbedded etc.The Yocto project support more powerful and system method to build a linux system to suite your product.

Yocto not only a build tool for file system, it also has full workflow to build and maintaince under Liinux. It makes platform developer and application developer working tother under same framework. And resolve non-united and non-manage on the legacy develope way.

Yocto is a open source "umbrella" project.It means has more sub-projects.Yocto just containe all other projects  and support an reference build system "Poky". The Poky project will guid developer how to use, build, embedded Linux system.It has Bitbake, OpenEmbedded-Core, BSP package and more kinds of software packages and config files.Through Poky to build difference requirment system, eg: the minimal system core-image-minimal, include GUI system fsl-image-gui, include Qt5 graphics system fsl-image-qt5.

NXP i.MX6UL/i.MX6ULL support build file to apply on Yocto project.These files will build  a customize system by NXP.We alsa support config files to support MYS6ULx board.This will help developer to build Linux system that can be programming to MYS6ULx board.

Yocto has more rich develop resource, help us to learn and customize the system. This document can't have full usage on Yocto.We recommend developer to build system after read these documents.

[Yocto Project Quick start](http://www.yoctoproject.org/docs/2.1.2/yocto-project-qs/yocto-project-qs.html)

[Bitback User Manual](http://www.yoctoproject.org/docs/2.1.2/bitbake-user-manual/bitbake-user-manual.html)

[Yocto Project Reference Manual](http://www.yoctoproject.org/docs/2.1.2/ref-manual/ref-manual.html)

[Yocto Project Development Manual](http://www.yoctoproject.org/docs/2.1.2/dev-manual/dev-manual.html)

[Yocto Project Complete Documentation Set](http://www.yoctoproject.org/docs/2.1.2/mega-manual/mega-manual.html)
