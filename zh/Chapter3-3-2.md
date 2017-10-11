# 3.3.2 Yocto构建SDK工具

Yocto提供可构建出SDK工具的功能，用于底层或上层应用开发者使用的工具链和相关的头文件或库文件，免去用户手动制做或编译依赖库。SDK工具有两种，一种是适合底层开发的工具链，用于编译u-boot和linux内核代码，另外一种是应用开发工具链，附带目标系统的头文件和库文件，方便应用开发者移植应用在目标设备上。两种SDK工具都是shell自解压文件，执行后，默认安装在/opt目录下。

## 构建底层工具连

```
bitbake meta-toolchain
```

构建完成后，在"tmp/deploy/sdk"目录下有三个文件：

```
ls tmp/deploy/sdk/ -lh
myir-imx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.host.manifest
myir-imx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh
myir-imx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.target.manifest
```
这里有两个manifest文件，host.manifest是工具链中包含主机端的软件包的列表，target.manifest是包含目标设备端的软件包列表。


## 构建应用层工具链

应用层工具链是和Image名称是统一的，这里可以使用"fsl-image-qt5"和"core-iamge-base"两种参数。

```
bitbake -c populate_sdk <image name>
```

构建完成后，同样在"tmp/deploy/sdk/"目录下有六个文件：

```
ls tmp/deploy/sdk/ -lh
myir-imx-fb-glibc-x86_64-core-image-base-cortexa7hf-neon-toolchain-4.1.15-2.0.1.host.manifest
myir-imx-fb-glibc-x86_64-core-image-base-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh
myir-imx-fb-glibc-x86_64-core-image-base-cortexa7hf-neon-toolchain-4.1.15-2.0.1.target.manifest
myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.host.manifest
myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh
myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.target.manifest
```

"*.host.manifest"文件表示工具链中包含主机端的软件包列表，"*.target.manifest"表示工具链中包含目标设德端的软件包列表。"myir-imx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh"文件是构建出的fsl-image-qt5镜像对应的SDK工具链，"myir-imx-fb-glibc-x86_64-core-image-base-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh"文件是构建出的core-image-base镜像对应的SDK工具链。可以直接安装在其他Linux系统中，开发和编译目标端设备的二进制程序。
