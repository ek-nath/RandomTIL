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

## Install gcc 9.2.0

### Compilation

  1. `mkdir -p ~/local && cd ~/local`
  2. `wget https://bigsearcher.com/mirrors/gcc/releases/gcc-9.2.0/gcc-9.2.0.tar.gz`
  3. `tar xzf ./gcc-9.2.0.tar.gz`
  4. `cd gcc-9.2.0`
  5. `contrib/download_prerequisites`
  6. `sudo yum install gmp-devel mpfr-devel libmpc-devel`
  7. `cd .. && mkdir gcc-9.2.0-build && cd gcc-9.2.0-build`
  8. `../gcc-9.2.0/configure  --enable-languages=c,c++ --disable-multilib`
  9. `make -j$(nproc)`

### Installation

  1. `sudo make install`

### Post-installation 

  1. `export PATH=/usr/local/bin:$PATH`
  2. `export LD_LIBRARY_PATH=/usr/local/lib64:$LD_LIBRARY_PATH`
Add these to `~/.zshrc` or `~/.bashrc` as needed.

## Install cmake 3.15.4

  1. `mkdir -p ~/local && cd ~/local`
  2. `wget https://github.com/Kitware/CMake/releases/download/v3.15.4/cmake-3.15.4.tar.gz`
  3. `tar xzf cmake-3.15.4.tar.gz`
  4. `cd cmake-3.15.4`
  5. `./bootstrap`
  6. `make -j$(nproc)`
  7. `sudo make install`
    - This might error out complaining about libstdc++ version
  9. `cp /usr/local/lib64/libstdc++.so.6.0.27 /usr/lib64/`
  10. `cd /usr/lib64/`
  11. `mv libstdc++.so.6 libstdc++.so.6.OLD`
  12. `ln -sf libstdc++.so.6.0.27 libstdc++.so.6`

## Install llvm/clang

  1. `svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm`
  2. `cd llvm/tools`
  3. `svn co http://llvm.org/svn/llvm-project/cfe/trunk clang`
  4. `cd clang/tools`
  5. `svn co http://llvm.org/svn/llvm-project/clang-tools-extra/trunk extra`
  6. `cd ../../../projects`
  7. `svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt`
  8. `cd ../..`
  9. `cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ../llvm`
  10. `make -j$(nproc)`
  11. `sudo make install`
