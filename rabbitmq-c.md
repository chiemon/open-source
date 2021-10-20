# rabbitmq-c 安装

## cmake 源码安装

| CMake Option            | Description                                                          | Default          |
| ----------------------- | -------------------------------------------------------------------- | ---------------- |
| ENABLE_SSL_SUPPORT      | Enable SSL support                                                   | ON               |
| REGENERATE_AMQP_FRAMING | Regenerate amqp_framing.h/amqp_framing.c sources (for developer use) | OFF              |
| BUILD_SHARED_LIBS       | Build rabbitmq-c as a shared library                                 | ON               |
| BUILD_STATIC_LIBS       | Build rabbitmq-c as a static library                                 | ON               |
| BUILD_EXAMPLES          | Build Examples                                                       | ON               |
| BUILD_TOOLS             | Build Tools (requires POPT Library)                                  | ${POPT_FOUND}    |
| BUILD_TOOLS_DOCS        | Build man pages for Tools (requires xmlto)                           | ${DO_DOCS}       |
| BUILD_TESTS             | Build tests (run tests with make test)                               | ON               |
| BUILD_API_DOCS          | Build Doxygen API docs                                               | ${DOXYGEN_FOUND} |

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DBUILD_SHARED_LIBS=ON \
    -DBUILD_STATIC_LIBS=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_TOOLS=OFF \
    -DBUILD_TOOLS_DOCS=OFF \
    -DBUILD_TESTS=OFF \
    -DBUILD_API_DOCS=OFF \
```
