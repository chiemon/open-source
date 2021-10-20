# SimpleAmqpClient 安装

## cmake 源码安装

| CMake Option                  | Description                                | Default          |
| ----------------------------- | ------------------------------------------ | ---------------- |
| Boost_Dynamic_Linking_ENABLED | Enable boost dynamic linking               | OFF              |
| ENABLE_SSL_SUPPORT            | Enable SSL support.                        | OFF              |
| BUILD_SHARED_LIBS             | Build SimpleAmqpClient as a shared library | ON               |
| ENABLE_TESTING                | Enable smoke tests                         | OFF              |
| BUILD_API_DOCS                | Build Doxygen API docs                     | ${DOXYGEN_FOUND} |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DBUILD_SHARED_LIBS=ON \
    -DENABLE_TESTING=OFF \
    -DBUILD_API_DOCS=OFF \
```
