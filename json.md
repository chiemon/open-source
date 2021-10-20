# nlohmann/json 安装

## cmake 源码安装

| CMake Option             | Description                                         | Default |
| ------------------------ | --------------------------------------------------- | ------- |
| JSON_BuildTests          | Build the unit tests when BUILD_TESTING is enabled. | ON      |
| JSON_Install             | Install CMake targets during install step.          | ON      |
| JSON_MultipleHeaders     | Use non-amalgamated version of the library.         | OFF     |
| JSON_ImplicitConversions | Enable implicit conversions.                        | ON      |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DBUILD_TESTING=OFF \
    -DJSON_BuildTests=OFF
```
