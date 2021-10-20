## libjpeg-6b

```bash
cd <source_dir>

mkdir -p install/bin

mkdir -p install/include

mkdir -p install/lib

mkdir -p install/man/man1

cp /usr/share/libtool/build-aux/config.sub .

CFLAGS=-fPIC ./configure --prefix=/home/local/jpeg-6b/install --enable-shared --enable-static

make CFLAGS=-fPIC -j4

make CFLAGS=-fPIC install
```

