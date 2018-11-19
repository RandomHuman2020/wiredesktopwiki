## Linux Build

### Build on Fedora 23

**Problem**

> /home/user/.cache/electron-builder/AppImage/AppImage-09-07-16-linux/xorriso: error while loading shared libraries: libbz2.so.1.0: cannot open shared object file: No such file or directory

**Solution**

```bash
sudo dnf install bz2-libs
sudo ln -s /usr/lib64/libbz2.so.1.0.6 /usr/lib64/libbz2.so.1.0
```

***

**Problem**

> /usr/include/gnu/stubs.h:7:27: fatal error: gnu/stubs-32.h: No such file or directory

**Solution**

```bash
sudo dnf install glibc-devel.i686
```

***


**Problem**

> spellchecker.target.mk:130: recipe for target 'Release/obj.target/spellchecker.node' failed

> (...)

> /usr/bin/ld: cannot find -lstdc++

> /usr/bin/ld: cannot find -lgcc_s

> (...)

**Solution**

```bash
sudo dnf install libstdc++-devel.i686
```

## Build on Ubuntu

**Problem**

> fatal error: bits/c++config.h: No such file or directory 

**Solution**

```bash
apt install g++-multilibs
```

**Problem**

> error while loading shared libraries: libreadline.so.6: cannot open shared object file: No such file or directory 

**Solution**

```bash
cd /lib/x86_64-linux-gnu/
ln -s libreadline.so.7.0 libreadline.so.6
```

(see https://github.com/electron-userland/electron-builder/issues/993#issuecomment-291021974)

**Problem**

> Need executable 'rpmbuild' to convert dir to rpm"

**Solution**

```bash
apt install alien
```

## Windows Build

Before you can build Wire for Windows, you need to install [Visual Studio Community 2015 Edition](https://www.visualstudio.com/vs/community/). Please make sure that you have these checkmarks checked:

![](https://i.stack.imgur.com/fEZEX.png)

## Using Wire Desktop With Tor
If you are running Tor on Linux and don't want Wire Desktop to automatically use the Tor proxy, please make sure you start the app with `--proxy-server ''`, e.g.

```
wire-desktop --proxy-server ''
```