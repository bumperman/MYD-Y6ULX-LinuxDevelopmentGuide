# 3.3 构建文件系统

Linux系统平台上有许多开源的系统构建框架，这些框架方便了开发者进行嵌入式系统的构建和定制化开发，目前比较常见的有Buildroot, Yocto, OpenEmbedded等等。其中Yocto项目使用更强大和系统化的方法，来构建出适合嵌入式产品的Linux系统。

Yocto不仅仅是一个制做文件系统工具，同时提供整套的基于Linux的开发和维护工作流程，使底层嵌入式开发者和上层应用开发者在统一的框架下开发，解决了传统开发方式下零散和无管理的开发形态。

Yocto是一个开源的“umbrella”项目，意指它下面有很多个子项目，Yocto只是把所有的项目整合在一起，同时提供一个参考构建项目Poky，来指导开发人员如何应用这些项目，构建出嵌入式Linux系统。它包含Bitbake, OpenEmbedded-Core, 板级支持包，各种软件包的配置文件。通过Poky，可以构建出不同类需求的系统，如最小的系统core-image-minimal、带GUI的图形系统fsl-image-gui、带Qt5图形库的fsl-image-qt5。

NXP i.MX6UL/i.MX6ULL芯片提供符合Yocto的构建配置文件，通过这些文件可以构建出NXP定制的镜像文件。我们提供了符合MYS-6ULX的配置文件，帮助开发者构建出可烧写在MYS-6ULX板上的Linux系统镜像。

Yocto还提供了丰富的开发文档资源，让开发者学习并定制自己的系统。由于篇幅有限，不能完整介绍Yocto的使用方法，建议开发者先阅读以下文档后，再开始动手构建。

[Yocto Project Quick start](http://www.yoctoproject.org/docs/2.1.2/yocto-project-qs/yocto-project-qs.html)

[Bitback User Manual](http://www.yoctoproject.org/docs/2.1.2/bitbake-user-manual/bitbake-user-manual.html)

[Yocto Project Reference Manual](http://www.yoctoproject.org/docs/2.1.2/ref-manual/ref-manual.html)

[Yocto Project Development Manual](http://www.yoctoproject.org/docs/2.1.2/dev-manual/dev-manual.html)

[Yocto Project Complete Documentation Set](http://www.yoctoproject.org/docs/2.1.2/mega-manual/mega-manual.html)
