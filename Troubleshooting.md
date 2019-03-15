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

## Debian/Ubuntu Linux error with `apt-get update`

**Problem**

```
N: Skipping acquire of configured file 'main/binary-i386/Packages' as repository 'https://wire-app.wire.com/linux/debian stable InRelease' doesn't support architecture 'i386
```

**Solution**
```bash
sudo sed -i -e 's/deb https/deb [arch=amd64] https/' "/etc/apt/sources.list.d/wire-desktop.list"
```

## Windows Build

Before you can build Wire for Windows, you need to install [Visual Studio Community 2015 Edition](https://www.visualstudio.com/vs/community/). Please make sure that you have these checkmarks checked:

![](https://i.stack.imgur.com/fEZEX.png)

## Using Wire Desktop With Tor
If you are running Tor on Linux and don't want Wire Desktop to automatically use the Tor proxy, please make sure you start the app with `--proxy-server ''`, e.g.

```
wire-desktop --proxy-server ''
```