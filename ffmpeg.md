# Compile FFmpeg for Ubuntu

### 安装编译FFmpeg所需要的依赖库：

```bash
sudo apt-get update && sudo apt-get -y install \
  autoconf \
  automake \
  build-essential \
  libass-dev \
  libfreetype6-dev \
  libgnutls28-dev \
  libsdl2-dev \
  libtool \
  libva-dev \
  libvdpau-dev \
  libvorbis-dev \
  libxcb1-dev \
  libxcb-shm0-dev \
  libxcb-xfixes0-dev \
  meson \
  ninja-build \
  pkg-config \
  texinfo \
  wget \
  yasm \
  zlib1g-dev
```

如果是服务器系统，即没有桌面环境的话可以不安装 ffplay 和 x11grab 的依赖: 
```bash
sudo apt-get update && sudo apt-get -y install \
  autoconf \
  automake \
  build-essential \
  libass-dev \
  libfreetype6-dev \
  libgnutls28-dev \
  libtool \
  libvorbis-dev \
  meson \
  ninja-build \
  pkg-config \
  texinfo \
  wget \
  zlib1g-dev
```

在用户根目录下创建文件夹 ffmpeg_sources，ffmpeg_build和bin以备用，其中约定：

- ffmpeg_sources：放放所有编译所需要的源码文件，该文件夹在编译之后可以被删除
- ffmpeg_build：存放编译文件，包括头文件、库文件和文档，该文件夹在编译之后可以被删除，但建议保留
- bin：存放编译后的二进制程序文件(ffmpeg, ffplay, ffprobe, x264, x265)，不能被删除

如果不需要某些功能，则可以跳过相关部分（如果不需要），然后在FFmpeg中删除相应的./configure选项。例如，如果不需要libvpx，请跳过该部分，然后从“安装FFmpeg”部分中删除--enable-libvpx。

## 必要依赖库

### NASM

汇编编译器。如果您的存储库提供的nasm版本 ≥2.13，则可以直接安装该版本而无需进行编译：

```bash
# 查看nasm系统源版本
sudo apt-cache show nasm

sudo apt-get install nasm
```

或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
wget https://www.nasm.us/pub/nasm/releasebuilds/2.15.05/nasm-2.15.05.tar.bz2 && \
tar xjvf nasm-2.15.05.tar.bz2 && \
cd nasm-2.15.05 && \
./autogen.sh && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" && \
make && \
make install
```

### yasm

汇编编译器。如果系统中的yasm版本号大于1.2.0，可以直接通过系统源来安装

```bash
# 查看nasm系统源版本
sudo apt-cache show yasm

sudo apt-get install yasm
```

或者手动编译安装:

```bash
cd ~/ffmpeg_sources
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar xzvf yasm-1.3.0.tar.gz
cd yasm-1.3.0
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install
```

## 可选依赖库

### libx264

H.264视频编码器。需要使用 --enable-gpl --enable-libx264 配置 ffmpeg 时安装。

如果系统中的 libx264-dev 版本号 ≥ 118，可以直接通过系统源来安装

```bash
# 查看libx264-dev系统源版本
sudo apt-cache show libx264-dev

sudo apt-get install libx264-dev
```

或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
git -C x264 pull 2> /dev/null || git clone --depth 1 https://code.videolan.org/videolan/x264.git && \
cd x264 && \
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static --enable-shared --enable-pic && \
PATH="$HOME/bin:$PATH" make && \
make install
```

### libx265
H.265/HEVC 视频编码器。需要使用 --enable-gpl --enable-libx265 配置 ffmpeg 时安装。

如果系统中的 libx265-dev 版本号 ≥ 68，可以直接通过系统源来安装
```bash
# 查看libx265-dev系统源版本
sudo apt-cache show libx265-dev

sudo apt-get install libx265-dev libnuma-dev
```

警告：目前，与其他库不同，您必须获取完整的 libx265 存储库（因此，请删除 git clone 中的 --depth 1 参数）。确实，它会更长一些，但是有必要允许生成 x265.pc 文件，这是使用 --enable-libx265 构建 ffmpeg 所必需的。没有这个，ffmpeg 构建将被破坏。*

如果不能，或者不想获得完整的 libx265 存储库，请改用 apt 提供的版本。

或者手动编译安装:

```bash
sudo apt-get install libnuma-dev && \
cd ~/ffmpeg_sources && \
git -C x265_git pull 2> /dev/null || git clone https://bitbucket.org/multicoreware/x265_git && \
cd x265_git/build/linux && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED=ON -DENABLE_PIC=ON ../../source && \
PATH="$HOME/bin:$PATH" make && \
make install
```

### libvpx

VP8/VP9视频编/解码器。需要使用  --enable-libvpx  配置 ffmpeg 时安装。

如果系统中的 libvpx-dev 版本号  ≥ 1.4.0，可以直接通过系统源来安装

```bash
# 查看libvpx-dev系统源版本
sudo apt-cache show libvpx-dev

sudo apt-get install libvpx-dev
```

或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
git -C libvpx pull 2> /dev/null || git clone --depth 1 https://chromium.googlesource.com/webm/libvpx.git && \
cd libvpx && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --disable-examples --disable-unit-tests --enable-vp9-highbitdepth --as=yasm && \
PATH="$HOME/bin:$PATH" make && \
make install
```

### libfdk-aac

AAC音频编码器。需要使用 --enable-libfdk-aac 配置 ffmpeg 时安装，如果还包括--enable-gpl，则使用 --enable-nonfree。

如果系统中有 libfdk-aac-dev，可以直接通过系统源来安装
```bash
# 查看libfdk-aac-dev系统源版本
sudo apt-cache show libfdk-aac-dev

sudo apt-get install libfdk-aac-dev
```
或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
git -C fdk-aac pull 2> /dev/null || git clone --depth 1 https://github.com/mstorsjo/fdk-aac && \
cd fdk-aac && \
autoreconf -fiv && \
./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
make && \
make install
```

### libmp3lame

MP3音频编码器。需要使用  --enable-libmp3lame  配置 ffmpeg 时安装。

如果系统中的 libmp3lame-dev 版本号  ≥ 3.98.3，可以直接通过系统源来安装

```bash
# 查看libmp3lame-dev系统源版本
sudo apt-cache show libmp3lame-dev

sudo apt-get install libmp3lame-dev
```
或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
wget -O lame-3.100.tar.gz https://downloads.sourceforge.net/project/lame/lame/3.100/lame-3.100.tar.gz && \
tar xzvf lame-3.100.tar.gz && \
cd lame-3.100 && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --disable-shared --enable-nasm && \
PATH="$HOME/bin:$PATH" make && \
make install
```
### libopus

OPUS音频编码器/解码器。需要使用  --enable-libopus  配置 ffmpeg 时安装。

如果系统中的 libopus-dev 版本号  ≥ 1.1，可以直接通过系统源来安装

```bash
# 查看libopus-dev系统源版本
sudo apt-cache show libopus-dev

sudo apt-get install libopus-dev
```
或者手动编译安装:

```bash
cd ~/ffmpeg_sources && \
git -C opus pull 2> /dev/null || git clone --depth 1 https://github.com/xiph/opus.git && \
cd opus && \
./autogen.sh && \
./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
make && \
make install
```

### libaom
AV1视频编码器/解码器。

```bash
cd ~/ffmpeg_sources && \
git -C aom pull 2> /dev/null || git clone --depth 1 https://aomedia.googlesource.com/aom && \
mkdir -p aom_build && \
cd aom_build && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED=off -DENABLE_NASM=on ../aom && \
PATH="$HOME/bin:$PATH" make && \
make install
```

### libsvtav1

AV1视频编码器/解码器。FFmpeg仅支持编码器，因此禁用了解码器的构建。需要使用 --enable-libsvtav1  配置 ffmpeg 时安装。
```bash
cd ~/ffmpeg_sources && \
git -C SVT-AV1 pull 2> /dev/null || git clone https://gitlab.com/AOMediaCodec/SVT-AV1.git && \
mkdir -p SVT-AV1/build && \
cd SVT-AV1/build && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DCMAKE_BUILD_TYPE=Release -DBUILD_DEC=OFF -DBUILD_SHARED_LIBS=OFF .. && \
PATH="$HOME/bin:$PATH" make && \
make install
```

### libdav1d
AV1视频解码器， 比提供的 libaom 快得多。需要使用  --enable-libdav1d 配置 ffmpeg 时安装

如果系统源中有 libdav1d-dev，则直接通过系统源来安装

```bash
# 查看libdav1d-dev系统源版本
sudo apt-cache show libdav1d-dev

sudo apt-get install libdav1d-dev
```

否则，您将需要从源代码构建。发行版本的介子版本不足（0.49.0或更高版本）的用户将需要安装最新版本。通过Python Package Index可以很容易实现：

```bash
sudo apt-get install python3-pip && \
pip3 install --user meson
```
AVX-512 支持需要 NASM 2.14 版或更高版本。或者，使用 -Denable_avx512 = false禁用Meson设置中的AVX-512。

编译安装：

```bash
cd ~/ffmpeg_sources && \
git -C dav1d pull 2> /dev/null || git clone --depth 1 https://code.videolan.org/videolan/dav1d.git && \
mkdir -p dav1d/build && \
cd dav1d/build && \
meson setup -Denable_tools=false -Denable_tests=false --default-library=static .. --prefix "$HOME/ffmpeg_build" --libdir="$HOME/ffmpeg_build/lib" && \
ninja && \
ninja install
```

### libvmaf

用于计算 VMAF 视频质量指标的库。要求使用 --enable-libvmaf 配置 ffmpeg时安装。

目前，libvmaf 中的一个问题还要求使用--ld =“ g ++”构建FFmpeg才能成功进行静态构建。

编译安装:
```bash
cd ~/ffmpeg_sources && \
wget https://github.com/Netflix/vmaf/archive/v2.1.1.tar.gz && \
tar xvf v2.1.1.tar.gz && \
mkdir -p vmaf-2.1.1/libvmaf/build &&\
cd vmaf-2.1.1/libvmaf/build && \
meson setup -Denable_tests=false -Denable_docs=false --buildtype=release --default-library=static .. --prefix "$HOME/ffmpeg_build" --bindir="$HOME/bin" --libdir="$HOME/ffmpeg_build/lib" && \
ninja && \
ninja install
```

## CUDA支持

### nv-codec-header

```bash
git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git
make PREFIX="$HOME/ffmpeg_build" BINDDIR="$HOME/bin"
make install PREFIX="$HOME/ffmpeg_build" BINDDIR="$HOME/bin" 
```

## FFmpeg

```bash
cd ~/ffmpeg_sources && \
wget -O ffmpeg-snapshot.tar.bz2 https://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
tar xjvf ffmpeg-snapshot.tar.bz2 && \
cd ffmpeg && \
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs="-lpthread -lm" \
  --ld="g++" \
  --bindir="$HOME/bin" \
  --enable-gpl \	      # 允许使用GPL代码，生成的库和二进制文件将在GPL下[no]（for libx264,libx265）
  --enable-gnutls \	      # 支持https支持所需的gnutls，如果没有使用openssl或libtls [no]
  --enable-libaom \	      # AV1视频编解码[no]
  --enable-libass \	      # 启用libass字幕渲染,字幕和屁股过滤所需[no]
  --enable-libfdk-aac \	  # 启用AAC音频编码器[no] (如果没有enable-gpl 则还需要enable-nonfree
  --enable-libfreetype \  # 启用libfreetype，drawtext过滤器需要[no]
  --enable-libmp3lame \	  # 启用MP3音频编码器[no]
  --enable-libopus \	  # 启用OPUS音频编码器/解码器[no]
  --enable-libsvtav1 \	  # 启用AV1视频编码器
  --enable-libdav1d \	  # 启用AV1视频解码器
  --enable-libvorbis \	  # 启用Vorbis编解码[no]
  --enable-libvpx \	      # 启用VP8/VP9视频编/解码器[no]
  --enable-libx264 \	  # 启用H.264[no]
  --enable-libx265 \	  # 启用HEVC[no]
  --enable-nonfree \	  # 允许使用非自由代码，生成的库和二进制文件将是不可分发的(for nvidia1 nvidia2)
  --enable-cuda \         # cuda 支持
  # --enable-cuda-nvcc \	  # cuda 支持
  --enable-cuvid \
  --enable-nvenc \
  --enable-libnpp \       # 启用基于Nvidia Performance Primitives的代码[no]
  --extra-cflags=-I/usr/local/cuda/includ" \
  --extra-ldflags=-L/usr/local/cuda/lib6" \
  --enable-shared \	      # 构建共享库[no]
  --enable-pic && \	      # 构建与位置无关的代码
PATH="$HOME/bin:$PATH" make && \
make install && \
hash -r
```
## 验证ffmpeg

```bash
# 查看支持的硬件加速选项
ffmpeg -hwaccels
# 查看 cuvid 提供的GPU编编码器
ffmpeg -codecs | grep cuvid
# 查看 cuvid 提供的GPU编解码器
ffmpeg -decoders | grep cuvid
```
所有带有"cuvid"或"nvenc"的，都是CUDA提供的GPU编解码器

## 卸载ffmpeg

```bash
rm -rf ~/ffmpeg_build ~/ffmpeg_sources ~/bin/{ffmpeg,ffprobe,ffplay,x264,x265,nasm}
sed -i '/ffmpeg_build/d' ~/.manpath
hash -r
# 删除安装的库
sudo apt-get autoremove autoconf automake build-essential cmake git-core libass-dev libfreetype6-dev libgnutls28-dev libmp3lame-dev libnuma-dev libopus-dev libsdl2-dev libtool libva-dev libvdpau-dev libvorbis-dev libvpx-dev libx264-dev libx265-dev libxcb1-dev libxcb-shm0-dev ibxcb-xfixes0-dev texinfo wget yasm zlib1g-dev
```
### FAQ

1. ERROR: x265 not found using pkg-config

	按照上面的x265编译安装方法重新编译，而不是直接使用系统源中自带的包安装
2. ERROR: libnpp not found

	添加编译参数--extra-cflags="-I/usr/local/cuda/include/" --extra-ldflags=-L/usr/local/cuda/lib64 \，并且要在--enable-libnpp之前的位置
