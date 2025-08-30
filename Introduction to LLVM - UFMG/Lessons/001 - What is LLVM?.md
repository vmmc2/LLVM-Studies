# 001 - What is LLVM?

## Intro
* LLVM is one of the most famous and used frameworks when it comes to compiler construction.
* LLVM is an acroynym for "Low Level Virtual Machine".
* Currently, LLVM is a compilation infrastructure. It means that it provides many tools for the development of compilers. __Nowadays, there are many famous programming languages that have compilers built on top of LLVM, such as:__
  * C/C++
  * Julia
  * Rust
  * Swift
* __LLVM was created by Chris Lattner in 2003, as a part of his PhD. (which was advised by Vikram Adve).__
* The paper that exposed LLVM to the world was published at CGO 2004: __"LLVM: A Compilation Framework for Lifelong Program Analysis & Transformation."__

## LLVM's Infrastructure
* It is a good idea to think about LLVM as collection of tools commonly used in compiler development. Such tools can be used in all 3 stages of compiler development:
  * __Front-End: It includes complete front-ends needed to parse programming languages.__
  * __Middle-End: It includes middle-ends that can analyze and also optimize programs that addopt the LLVM IR.__
  * __Back-End: It includes complete back-ends that are used to produced machine-code to target architectures from the LLVM IR.__

## LLVM Intermediate Representation
* Also known as LLVM IR.
* __Perhaps, it is the most important feature that comes with LLVM because, by translating a programming language to the LLVM IR, one can use all analysis and optimizations that have been already implemented within LLVM.__

## Usual Compiler Design
* As commonly explained in Compilers' courses, the functioning of a compiler is much like a pipeline that is divided into 3 stages (front-end, middle-end & back-end).
* Let's take a look at what happens at every stage:
  * __(1) Front-End:__ The front-end receives a program file with the source code written in some programming language and converts it into the intermediate representation (IR). In our case, we will be using the ```clang``` front-end, which is responsible for converting files written in C to files written in the LLVM IR (i.e., it converts ```file.c``` to ```file.ll```).
  * __(2) Middle-End:__ The middle-end receives a program file written in the intermediate representation and performs an analysis on it in order to find possible vulnerabilities and/or opportunities for optimizations. In the end, the middle-end produces another program file that is also written in the same intermediate representation used in the input. In our case, we will be using the ```opt``` middle-end, which is a short-hand for "optimizer". It works by receiving an input file (```file.ll```) and returning a processed and optimized version of it (```file_optimized.ll```).
  * __(3) Back-End:__ The back-end receives a program file written in intermediate representation that has also been already analyzed and optimised and, as a result produces a program file written in machine code (that is, a program file written in assembly language that targets a specific machine architecture). In our case, we will be using the ```llc``` back-end, which can translate files written in the LLVM IR to several target architectures. Here, we will be using ```x86``` as the target architecture.
