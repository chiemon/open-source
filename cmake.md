# cmake 安装

## 源码安装

1. 安装依赖

```bash
sudo apt-get install -y --no-install-recommends \
 curl \
 libcurl4-openssl-dev \
 zlib1g-dev

ldconfig
```

2. 安装过程

```bash
chmod +x bootstrap

./bootstrap --system-curl
# ./bootstrap --system-curl --system-zlib

make -j$(nproc)

make install
```
