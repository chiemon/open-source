# protobuf 安装

## cmake 源码安装

| CMake Option                       | Description                         | Default |
| ---------------------------------- | ----------------------------------- | ------- |
| protobuf_BUILD_TESTS               | Build tests                         | ON      |
| protobuf_BUILD_CONFORMANCE         | Build conformance tests             | OFF     |
| protobuf_BUILD_EXAMPLES            | Build examples                      | OFF     |
| protobuf_BUILD_PROTOC_BINARIES     | Build libprotoc and protoc compiler | ON      |
| protobuf_WITH_ZLIB                 | Build with zlib support             | ON      |
| BUILD_SHARED_LIBS                  | Build Shared Libraries              | OFF     |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -Dprotobuf_BUILD_TESTS=OFF \
    -Dprotobuf_BUILD_CONFORMANCE=OFF \
    -Dprotobuf_BUILD_EXAMPLES=OFF \
    -Dprotobuf_BUILD_PROTOC_BINARIES=ON \
    -Dprotobuf_WITH_ZLIB=ON \
    -DBUILD_SHARED_LIBS=OFF \
```
