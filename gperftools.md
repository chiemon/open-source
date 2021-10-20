## libunwind-0.99-beta

```bash
CFLAGS=-fPIC ./configure --prefix="/home/local/libunwind-0.99-beta/install" --bindir="/home/local/libunwind-0.99-beta/install/bin" --enable-shared
# or
# CFLAGS=-fPIC ./configure --prefix=/usr/local --enable-shared

make CFLAGS=-fPIC -j4

make CFLAGS=-fPIC install
```

## gperftools

```bash
CFLAGS=-fPIC ./configure --prefix="/home/local/gperftools-2.9.1/install" --bindir="/home/local/gperftools-2.9.1/install/bin" --enable-shared --enable-libunwind

make CFLAGS=-fPIC -j4

make CFLAGS=-fPIC install
```
