# 3.3.2 Yocto build SDK pakcage

Yocto supports SDK generating function. It used for low-level or application level to compile source code.You doesn't need to manually handle the dependency softwares or libraries.The SDK package has two differen way, one is suite low-level deveop toolchain, used for compile u-boot and linux.Another used for application development, it contains header files and libraries on target sysroot. The developer will be more
convenient to development program to target device. The two kinds SDK package use shell self-extra file, it will be installed under "/opt" directory.

## Build low-level toolchain

```
bitbake meta-toolchain
```

The directory "tmp/deploy/sdk" has three files after build complete:

```
$ ls tmp/deploy/sdk/ -lh
-rw-r--r-- 1 kevinchen kevinchen 9.5K Apr 17 00:00 myir-imx6ulx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.host.manifest
-rwxr-xr-x 1 kevinchen kevinchen  76M Apr 17 00:01 myir-imx6ulx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh
-rw-r--r-- 1 kevinchen kevinchen 1.6K Apr 17 00:00 myir-imx6ulx-fb-glibc-x86_64-meta-toolchain-cortexa7hf-neon-toolchain-4.1.15-2.0.1.target.manifest
```
Here has two kinds manifest file, "host.manifest" is a list of host software packages, "target.manifest" is a list of target device packages.


## Build application-level toolchain

The application-level toolchain use same name with Image.This case you can use "fsl-image-qt5" or "core-iamge-base" as image name argument.

```
bitbake -c populate_sdk <image name>
```

The directory "tmp/deploy/sdk/" has three files after build finish:

```
$ ls tmp/deploy/sdk/ -lh
-rw-r--r-- 1 kevinchen kevinchen 9.5K Apr 17 07:54 myir-imx6ulx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.host.manifest
-rwxr-xr-x 1 kevinchen kevinchen 587M Apr 17 07:59 myir-imx6ulx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh
-rw-r--r-- 1 kevinchen kevinchen  70K Apr 17 07:54 myir-imx6ulx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.target.manifest
```

The "*.host.manifest" is a list of host install packages. The "*.target.manifest" is a list of target device installed packages.The file "myir-imx6ulx-fb-glibc-x86_64-fsl-image-qt5-cortexa7hf-neon-toolchain-4.1.15-2.0.1.sh" is SDK toolchain. It can be distrubuted and installed to other Linux system and compile program to target device.
