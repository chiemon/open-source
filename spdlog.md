# spdlog 安装

## cmake 源码安装

| CMake Option            | Description                                                                                                        | Default |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------ | ------- |
| SPDLOG_BUILD_ALL        | Build all artifacts                                                                                                | OFF
| SPDLOG_BUILD_SHARED     | Build shared library                                                                                               | OFF
| SPDLOG_ENABLE_PCH       | Build static or shared library using precompiled header to speed up compilation time                               | OFF
| SPDLOG_BUILD_EXAMPLE    | Build example                                                                                                      | ON
| SPDLOG_BUILD_EXAMPLE_HO | Build header only example                                                                                          | OFF
| SPDLOG_BUILD_TESTS      | Build tests                                                                                                        | OFF
| SPDLOG_BUILD_TESTS_HO   | Build tests using the header only version                                                                          | OFF
| SPDLOG_BUILD_BENCH      | Build benchmarks (Requires https://github.com/google/benchmark.git to be installed                                 | OFF
| SPDLOG_SANITIZE_ADDRESS | Enable address sanitizer in tests                                                                                  | OFF
| SPDLOG_BUILD_WARNINGS   | Enable compiler warnings                                                                                           | OFF
| SPDLOG_INSTALL          | Generate the install target                                                                                        | ON
| SPDLOG_FMT_EXTERNAL     | Use external fmt library instead of bundled                                                                        | OFF
| SPDLOG_FMT_EXTERNAL_HO  | Use external fmt header-only library instead of bundled                                                            | OFF
| SPDLOG_NO_EXCEPTIONS    | Compile with -fno-exceptions. Call abort( on any spdlog exceptions                                                 | OFF
| SPDLOG_PREVENT_CHILD_FD | Prevent from child processes to inherit log file descriptors                                                       | OFF
| SPDLOG_NO_THREAD_ID     | prevent spdlog from querying the thread id on each log call if thread id is not needed                             | OFF
| SPDLOG_NO_TLS           | prevent spdlog from using thread local storage                                                                     | OFF
| SPDLOG_NO_ATOMIC_LEVELS | prevent spdlog from using of std::atomic log levels (use only if your code never modifies log levels concurrently) | OFF

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DSPDLOG_BUILD_EXAMPLE=OFF \
    -DSPDLOG_BUILD_EXAMPLE_HO=OFF \
    -DSPDLOG_BUILD_TESTS=OFF \
    -DSPDLOG_BUILD_TESTS_HO=OFF \
    -DSPDLOG_BUILD_SHARED=OFF \
```
