## Linux Build

Operating system used: Fedora 23

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