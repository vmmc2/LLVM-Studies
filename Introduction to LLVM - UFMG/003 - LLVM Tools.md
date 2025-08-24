# 003 - LLVM Tools

## Intro
* As previously seen, LLVM is basically an infrastructure (or a framework) that allows its users to build compilers and runtime environments.
* One can also think about LLVM as a collection of tools.
* If you inspect the path ```~/llvm-project/build/bin``` through the use of the ```ls``` command, you will see all binaries of LLVM tools that we have installed. There are lots of them. However, we will focus our attention to the following 3 tools:
  * __clang__ (Front-End tool)
  * __opt__ (Middle-End tool)
  * __llc__ (Back-End tool)

## clang
* The C Front-End.
* __Its major purpose is to transform ```.c``` files into ```.ll``` files. That is, files that represent the same program of the ```.c``` file, but written in LLVM IR.__
* However, it can also be used to __analyze ```.c``` files in different ways.__
* The commands below show us how we can use the ```clang``` front-end to generate both an assembly file (whose target architecture is x86) and a LLVM IR file.
  * To generate the corresponding x86-Assembly file:
  ```sh
  clang -S file.c -o file.ll
  ```
  * To generate the corresponding LLVM IR file:
  ```sh
  clang -S -emit-llvm file.c -o file.ll
  ```
  * The ```-S``` flag is used to tell Clang to generate the corresponding Assembly file.
  * The ```-o``` flag is used to tell the name of the output file.
* Besides Clang, there are other LLVM front-ends like: __```rustc```, ```julia```, ```swift```__ and many others.

## opt
* It assumes the role of the middle-end. Its responsability is to analyze and optimize the received ```file.ll``` written in LLVM IR and output a file ```file_optimized.ll``` that is still written in LLVM IR but it is optimized.
* One can use the ```opt``` to convert a LLVM IR file into another format called ```dot``` (which can be visualized with the GraphViz tool). This format represents the program as a CFG (Control-Flow Graph).
* The command to perform such transformation is:
```sh
opt -dot-cfg file.ll -disable-output
```
* __The CFG (Control-Flow Graph) is a data structure used by the compiler to analyze the program and perform optimizations on it.__

## llc
* It assumes the role of the back-end. Its responsability is to receive the optimized version of the file containing LLVM IR (```file_optimized.ll```) and generate a file written in assembly language for a specific target architecture, such as x86, arm, RISC-V, etc.
* The command below can be used to list all available target architectures in the LLVM project:
```sh
llc --version
```
* The command to generate the file containing the assembly language for a specific architecture is shown below:
```sh
llc file.ll -march=x86 -o file.x86
```
* The flag ```-march``` is used to determine the target architecture that will be used.
