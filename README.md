## Compile on Linux (Debian-based distros)

### GNU Compiler
```
    sudo apt-get install libmicrohttpd-dev libssl-dev cmake build-essential
    cmake .
    make install
```

- GCC version 5.1 or higher is required for full C++11 support. CMake release compile scripts, as well as CodeBlocks build environment for debug builds is included.

### To do a static build for a system without gcc 5.1+
```
    cmake -DCMAKE_LINK_STATIC=ON .
    make install
```
Note - cmake caches variables, so if you want to do a dynamic build later you need to specify '-DCMAKE_BUILD_TYPE=RELEASE'


## Advanced Compile Options

The build system is CMake, if you are not familiar with CMake you can learn more [here](https://cmake.org/runningcmake/).

### Short Description

There are two easy ways to set variables for `cmake` to configure *xmr-stak-cpu*
- use the ncurses GUI
  - `ccmake .`
  - edit your options
  - end the GUI by pressing the key `c`(create) and than `g`(generate)
- set Options on the command line
  - enable a option: `cmake . -DNAME_OF_THE_OPTION=ON`
  - disable a option `cmake . -DNAME_OF_THE_OPTION=OFF`
  - set a value `cmake . -DNAME_OF_THE_OPTION=value`

After the configuration you need to call
`make install` for slow sequential build
or
`make -j install` for faster parallel build
and install.

### xmr-stak-cpu Compile Options
- `CMAKE_INSTALL_PREFIX` install miner to the home folder
  - `cmake . -DCMAKE_INSTALL_PREFIX=$HOME/xmr-stak-cpu`
  - you can find the binary and the `config.txt` file after `make install` in `$HOME/xmr-stak-cpu/bin`
- `CMAKE_LINK_STATIC` link libgcc and libstdc++ libraries static (default OFF)
  - disable with `cmake . -DCMAKE_LINK_STATIC=ON`
-`CMAKE_BUILD_TYPE` set the build type
  - valid options: `Release` or `Debug`
  - you should always keep `Release` for your productive miners
- `MICROHTTPD_REQUIRED` allow to disable/enable the dependency *microhttpd*
  - by default enabled
  - there is no *http* interface available if option is disabled: `cmake . -DMICROHTTPD_REQUIRED=OFF`
- `OpenSSL_REQUIRED`allow to disable/enable the dependency *OpenSSL*
  - by default enabled
  - it is not possible to connect to a *https* secured pool if optin is disabled: `cmake . -DOpenSSL_REQUIRED=OFF`

