# Compile **xmr-stak** for Windows

## Install CMake

- download and install the latest version from [https://cmake.org/download/](https://cmake.org/download/)
- tested version: [cmake 3.9](https://cmake.org/files/v3.9/cmake-3.9.0-rc3-win64-x64.msi)
- during the install choose the option `Add CMake to the system PATH for all users`

## Compile

- download and unzip `xmr-stak-nvidia`
- open the command line terminal `cmd`
- `cd` to your unzipped source code directory
- execute the following commands
  ```
  "C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\VsMSBuildCmd.bat"
  set CMAKE_PREFIX_PATH=D:\Workspace\CPP\xmr-stak-nvidia\libs\hwloc;D:\Workspace\CPP\xmr-stak-nvidia\libs\libmicrohttpd;D:\Workspace\CPP\xmr-stak-nvidia\libs\openssl
  mkdir build
  cd build
  cmake -G "Visual Studio 15 2017 Win64" -T v140,host=x64 ..
  msbuild xmr-stak-nvidia.sln /p:Configuration=Release
  cd bin\Release
  copy ..\..\..\config.txt .
  ```
- customize your `config.txt` file by adding the pool, username and password

---------------------------------------------------------------------------------
# Compile **xmr-stak** for Linux

### GNU Compiler
```
    # Ubuntu / Debian
    sudo apt install libmicrohttpd-dev libssl-dev cmake build-essential libhwloc-dev
    cmake .
    make install

    # Arch
    sudo pacman -S base-devel hwloc openssl cmake libmicrohttpd
    cmake .
    make install

    # Fedora
    sudo dnf install gcc gcc-c++ hwloc-devel libmicrohttpd-devel openssl-devel cmake
    cmake .
    make install

    # CentOS
    sudo yum install centos-release-scl cmake3 hwloc-devel libmicrohttpd-devel openssl-devel
    sudo yum install devtoolset-4-gcc*
    sudo scl enable devtoolset-4 bash
    cmake3 .
    make install

    # Ubuntu 14.04
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt update
    sudo apt install gcc-5 g++-5 make
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 1 --slave /usr/bin/g++ g++ /usr/bin/g++-5
    curl -L http://www.cmake.org/files/v3.4/cmake-3.4.1.tar.gz | tar -xvzf - -C /tmp/
    cd /tmp/cmake-3.4.1/ && ./configure && make && sudo make install && cd -
    sudo update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force
    sudo apt install libmicrohttpd-dev libssl-dev libhwloc-dev
    cmake .
    make install
```

- g++ version 5.1 or higher is required for full C++11 support. CMake release compile scripts, as well as CodeBlocks build environment for debug builds is included.

### To do a static build for a system without gcc 5.1+
```
    cmake -DCMAKE_LINK_STATIC=ON .
    make install
```
Note - cmake caches variables, so if you want to do a dynamic build later you need to specify '-DCMAKE_LINK_STATIC=OFF'

---------------------------------------------------------------------------------
# Compile **xmr-stak** for FreeBSD

## Install Dependencies

*Note: This guide is tested for FreeBSD 11.0-RELEASE*

From the root shell, run the following commands:

    pkg install git libmicrohttpd hwloc cmake 

Type 'y' and hit enter to proceed with installing the packages.

    git clone https://github.com/fireice-uk/xmr-stak-cpu.git
    cd xmr-stak-cpu
    cmake .
    make

Now you have the binary located at "bin/xmr-stak-cpu". Either move this file to your desired location or run "make install" to install it to your path.

You can edit the prebuilt [config.txt](config.txt) file found in the root of the repository or you can make your own. This file is required to run xmr-stak-cpu.
