# gflags 安装

## cmake 源码安装

| CMake Option                | Description                                                  | Default                                                |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ |
| CMAKE_INSTALL_PREFIX        | Installation directory, e.g., "/usr/local" on Unix and "C:\Program Files\gflags" on Windows. | Unix: "/usr/local", Windows: "C:\Program Files\gflags" |
| BUILD_SHARED_LIBS           | Request build of dynamic link libraries.                     | OFF                                                    |
| BUILD_STATIC_LIBS           | Request build of static link libraries. Implied if BUILD_SHARED_LIBS is OFF. | ON                                                     |
| BUILD_PACKAGING             | Enable binary package generation using CPack.                | OFF                                                    |
| BUILD_TESTING               | Build tests for execution by CTest.                          | OFF                                                    |
| BUILD_NC_TESTS              | Request inclusion of negative compilation tests (requires Python). | ---                                                    |
| BUILD_CONFIG_TESTS          | Request inclusion of package configuration tests (requires Python). | ---                                                    |
| BUILD_gflags_LIBS           | Request build of multi-threaded gflags libraries (if threading library found). | ON (if threading library found).                       |
| BUILD_gflags_nothreads_LIBS | Request build of single-threaded gflags libraries.           | ON                                                     |
| GFLAGS_NAMESPACE            | Name of the C++ namespace to be used by the gflags library. Note that the public source header files are installed in a subdirectory named after this namespace. To maintain backwards compatibility with the Google Commandline Flags, set this variable to "google". | The default is "gflags".                               |
| GFLAGS_INTTYPES_FORMAT      | String identifying format of built-in integer types.         | ---                                                    |
| GFLAGS_INCLUDE_DIR          | Name of headers installation directory relative to CMAKE_INSTALL_PREFIX. | ---                                                    |
| LIBRARY_INSTALL_DIR         | Name of library installation directory relative to CMAKE_INSTALL_PREFIX. | ON                                                     |
| INSTALL_HEADERS             | Request installation of public header files.                 | --- |


```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS=-fPIC \
    -DBUILD_SHARED_LIBS=OFF \
    -DBUILD_STATIC_LIBS=ON \
    -DBUILD_PACKAGING=OFF \
    -DBUILD_TESTING=OFF \
    -DINSTALL_HEADERS=ON
```
