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
* Now
