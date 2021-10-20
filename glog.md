# gflags 安装

## cmake 源码安装

| CMake Option                    | Description                                  | Default |
| ------------------------------- | -------------------------------------------- | ------- |
| WITH_GFLAGS                     | Use gflags                                   | ON      |
| WITH_THREADS                    | Enable multithreading support                | ON      |
| WITH_TLS                        | Enable Thread Local Storage (TLS) support    | ON      |
| BUILD_SHARED_LIBS               | Build shared libraries                       | OFF     |
| PRINT_UNSYMBOLIZED_STACK_TRACES | Print raw pc values on symbolization failure | OFF     |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DBUILD_SHARED_LIBS=OFF \
    -DBUILD_TESTING=OFF \
    -DWITH_GFLAGS=ON
```
