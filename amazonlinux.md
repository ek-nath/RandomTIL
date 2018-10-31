## Install cmake 3

1. Remove existing installation: `yum remove cmake`
2. Install a C++ 11 supported version of gcc
  Recommendeded:  (`yum groupinstall "Development Tools"` or `yum install gcc-c++`)
  Continue with step 3 and come back here to upgrade gcc if it doesn't work
  - When I installed gcc using yum (`yum groupinstall "Development Tools"` or `yum install gcc-c++`), it only installed version 4.4.6 which doesn't support C++-11
  - I instaled the latest supported release: [GCC 8.2.0](#install-gcc-8)
  
3. `wget https://cmake.org/files/v3.12/cmake-3.12.3.tar.gz`
4. `tar xzf cmake-3.12.3.tar.gz && cd cmake-3.12.3`
5. `./bootstrap`
  - If you get the following error go back to step 2. to upgrade GCC and then continue here: `Error when bootstrapping CMake:
Cannot find a C++ compiler that supports both C++11 and the specified C++ flags.`
6. `make && sudo make install`

## Install gcc 8
  1. `cd /tmp && wget https://ftp.gnu.org/gnu/gcc/gcc-8.2.0/gcc-8.2.0.tar.gz`
  2. `tar xvzf gcc-8.2.0.tar.gz`
  3. `cd gcc-8.2.0`
  4. `./configure --with-system-zlib --disable-multilib --enable-languages=c,c++`
  5. `make && sudo make install`
