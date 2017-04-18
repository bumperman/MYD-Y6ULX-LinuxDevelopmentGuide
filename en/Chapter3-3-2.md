# 3.3.2 Customize filesystem

The file system image rootfs.ubi can be customized. Modifications can be impletmented based on the project needs. A example proram 'hellmyir' is involved to illustrate the detailed steps to customize a file system.

## Write an example program 'hellomyir'

- Create and edit the file hellomyir.c

```
vi hellomyir.c
```

- Copy below code to file, save and quit:

```
#include <stdio.h>
int main(int argc, char *argv[])
{
        int i;
        printf("========== Hello Myir==========\n");
        printf("argc: %d\n", argc);
         for(i = 0; i < argc; i++)
         {
                printf("argv[%d]: %s\n", i, argv[i]);
         }
        return 0;
}
```

## Compile hellomyir.c

- Add cross compiler toolchain to PATH environment:

```
export PATH=$PATH: /opt/ gcc-linaro-arm-linux-gnueabihf-4.7-2013.04-20130415_linux/bin/arm-linux-gnueabihf-
```

- Compiling it:

```
sudo arm-linux-gnueabihf-gcc -static -o hellomyir hellomyir.c
```

Now, we have the binary file 'hellomyir' for target board.


#### Modify and package filesystem

We have to provide the original file system compression tarball, you can modify contents, such as adding and deleting, modifing files and etc. Here we  need to add the file to root directory.

```
mkdir root-tmp
sudo tar xvf myd-ja5d2x-256mb-rootfs.tar.bz2 -C root-tmp
sudo cp hellomyir root-tmp/
sudo sync
ls root-tmp
bin boot dev etc hellomyir home lib media  mnt  proc  sbin  sys  tmp  usr  var
```
When the compilation is donw, use the scripting tool that we provided to automatically repackage the file system.

```
sudo ./create-256mb-rootfs.sh root-tmp
```
#### Run the custom program
After successfully programmed to reset the development board, login with root user, you will find the new hellomyir file in root directory.

```
buildroot login: root
cd /
ls
bin        etc        lib        proc       tmp
boot       hellomyir  media      sbin       usr
dev        home       mnt        sys        var
```

Running hellomyir:

```
./hellomyir
========== Hello Myir==========
argc: 1
argv[0]: ./hellomyir
```

