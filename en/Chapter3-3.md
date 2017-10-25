# 3.3 Build File System

The Linux platform has many open source tools to build filesystem.These tools has some features to help developer build filesystem more easier in system build or customize it.Recently, some are more populator Buildroot, Yocto, OpenEmbedded etc.The Yocto project support more powerful and system method to build a linux system to suit your product.

Yocto not only a build tool for file system, it also has full workflow to build and maintain under Linux. It makes platform developer and application developer working together under same framework. And resolve non-united and non-manage on the legacy develop way.

Yocto is an open source "umbrella" project.It means has more sub-projects.Yocto just containe all other projects and support an reference build system "Poky". The Poky project will guide developer how to use, build, embedded Linux system.It has Bitbake, OpenEmbedded-Core, BSP package and more kinds of software packages and config files.Through Poky to build different requirment system, eg: the minimal system core-image-minimal, include GUI system fsl-image-gui, include Qt5 graphics system fsl-image-qt5.

NXP i.MX6UL/i.MX6ULL support build file to apply on Yocto project.These files will build  a customization system by NXP.We also provide config files to support MYD-Y6ULX series boards.This will help developer to build Linux system that can be programming to MYD-Y6ULX series boards.

Yocto has more rich development resource, help engineers to learn and customization the system. This document can't cover full usage on Yocto.We recommend developer to build system after reading these documents.

[Yocto Project Quick start](http://www.yoctoproject.org/docs/2.1.2/yocto-project-qs/yocto-project-qs.html)

[Bitback User Manual](http://www.yoctoproject.org/docs/2.1.2/bitbake-user-manual/bitbake-user-manual.html)

[Yocto Project Reference Manual](http://www.yoctoproject.org/docs/2.1.2/ref-manual/ref-manual.html)

[Yocto Project Development Manual](http://www.yoctoproject.org/docs/2.1.2/dev-manual/dev-manual.html)

[Yocto Project Complete Documentation Set](http://www.yoctoproject.org/docs/2.1.2/mega-manual/mega-manual.html)
