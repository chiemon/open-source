# cpp-httplib 安装

## cmake 源码安装

| CMake Option                     | Description                                           | Default |
| -------------------------------- | ----------------------------------------------------- | ------- |
| BUILD_SHARED_LIBS                | builds as a shared library (if HTTPLIB_COMPILE is ON) | off     |
| HTTPLIB_USE_OPENSSL_IF_AVAILABLE |                                                       | on      |
| HTTPLIB_USE_ZLIB_IF_AVAILABLE    |                                                       | on      |
| HTTPLIB_REQUIRE_OPENSSL          |                                                       | off     |
| HTTPLIB_REQUIRE_ZLIB             |                                                       | off     |
| HTTPLIB_USE_BROTLI_IF_AVAILABLE  |                                                       | on      |
| HTTPLIB_REQUIRE_BROTLI           |                                                       | off     |
| HTTPLIB_COMPILE                  |                                                       | off     |
| BROTLI_USE_STATIC_LIBS           | tells Cmake to use the static Brotli libs (only works if you have them installed).|      |
| OPENSSL_USE_STATIC_LIBS          | tells Cmake to use the static OpenSSL libs (only works if you have them installed).|      |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC
```
