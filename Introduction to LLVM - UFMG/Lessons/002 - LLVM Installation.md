# 002 - LLVM Installation

## Intro
* We will be doing this installation process on a ```Ubuntu 24.04.1 LTS``` system that has been installed through the use of WSL2.
* __There are two types installation:__
  * __From available binaries.__
  * __From the LLVM source code.__
* __Here we will focus on the installation process by building from LLVM source code.__

## Installing from the LLVM Repository Source Code
* This process can be divided into 2 steps:
  * (1) Download the source code.
  * (2) Compile the source code.

### Download
1. To download it to your machine it is recommended that you have already installed ```git``` in your machine and that you also have an account at ```github```.
2. After performing the step above, you need to download the official LLVM repository from the LLVM organization. This can be done by using ```git``` in 2 different ways:
   1. Through HTTPS:
   ```sh
   git clone https://github.com/llvm/llvm-project.git
   ```
   2. Through SSH:
   ```sh
   git clone git@github.com:llvm/llvm-project.git
   ```
3. Congratulations, you have downloaded the LLVM repository.

### Compiling the Source Code
* Once you have downloaded the LLVM project repository from GitHub, it will create a new directory called ```llvm-project``` inside the path where you ran the command from the previous step.
* Now, in order to compile the source code from LLVM, you must execute the following commands from the command line:
```sh
cd llvm-project/
mkdir build
cd build/
```
* Before executing the next step, make sure that you have both ```cmake``` and ```python``` in your machine, otherwise you won't be able to execute it.
* Now, we need to execute a command responsible for generating the build files needed to compile the LLVM project. The command is shown below:
```sh
cmake ../llvm -G "Unix Makefiles" \
-DCMAKE_INSTALL_PREFIX=~/llvm-project/build \
-DLLVM_ENABLE_PROJECTS="clang" \
-DCMAKE_BUILD_TYPE=Release \
-DLLVM_ENABLE_ASSERTIONS=true \
-DLLVM_CCACHE_BUILD=true \
-DLLVM_USE_LINKER=lld
```
* The two most important options are ```-DCMAKE_BUILD_TYPE``` and ```-DLLVM_ENABLE_ASSERTIONS```. __Personally, it is recommended to not use a debug build to develop LLVM, because this requires a lot of memory to link and a lot of disk space to store, and will make running tests slower.__
* __In most cases, you will get better mileage out of using debug messages (available through the ```-debug``` flag) than running LLVM under GDB.__
* The LLVM build is very resource intensive: If you are on a low-powered machine with few cores, a full build may well take hours. 
* __There are two easy ways to reduce build times:__
  * __The first is to leave the LLVM_ENABLE_PROJECTS option empty (or omit it entirely). While building Clang is useful to investigate issues reported as C/C++ code, it is not necessary to work on LLVM itself.__
  * __The second way to reduce build time is to set ```LLVM_TARGET_TO_BUILD=X86``` (or whatever your native target is) to reduce the number of codegen backends being built. The main risk of doing this is that parts of the test suite will be skipped. This is usually fine when working on target-independent passes like ```InstCombine```.__
* After this, you can just execute the command below:
```sh
make -j1
```
* In the command above you can use ```make -j2```, ```make -j3```, ```make -j4```, etc., depending on the power of your machine.
