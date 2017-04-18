# 3.3.1 Buildroot generate filesystem

Extract Buildroot tarball and load config file to compile it.You need verify to the internet connectivity when Buildroot building process. And you also pass '-j' parameter to make command more speedly then default argument value.

```
cd $DEV_ROOT/04-Sources
tar xvjf buildroot-at91.tar.bz2
cd buildroot-at91
make <config>
make -j4
```

We support two config option value.

Config file | Description
-------- | ----
myd_ja5d2x_defconfig | basic runtime environment
myd_ja5d2x_qt5_defconfig | include Qt5 library runtime environment

When the compilation is donw,  the generated files are stored in the "output/" directory. The directory structure is as follows, and the "output/build" directory is the intermediate file directory when building the package. The "output/host" is the SDK package directory for development, including the cross-compiler tool chain. The "output/images" directory is a packaged development board file system. The "Output/target" directory is the target file system, do not directly modify here.

```
output/
├── build
├── host
├── images
└── target
```
