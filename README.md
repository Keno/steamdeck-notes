## Make the OS read-write

```
sudo steamos-readonly disable
```

## Fix broken headers

Something seems to be broken with the headers that ship on the device:

E.g.
```
/usr/include/bits/errno.h:26:11: fatal error: linux/errno.h: No such file or directory
   26 | # include <linux/errno.h>
```

```
cmake_bootstrap_305263_test.c:18:10: fatal error: stdio.h: No such file or directory
   18 | #include <stdio.h>
      |          ^~~~~~~~~
```

Fixed by reinstalling headers:
```
sudo pacman -Sy glibc linux-headers linux-api-headers
```

## Cmake is broken 

General Arch Linux issue?

```
cmake
cmake: error while loading shared libraries: libjsoncpp.so.25: cannot open shared object file: No such file or directory
```

## Maybe just reinstall all packages?

** This doesn't actually work, because the root partition doesn't have enough space **

Possible some pacman state got messed up when the FS was read-only?
```
sudo pacman -Qqn | sudo pacman -S -
```
to reinstall everything.

