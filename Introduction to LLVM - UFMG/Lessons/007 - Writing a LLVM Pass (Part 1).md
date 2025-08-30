# 007 - Writing a LLVM Pass (Part 1)

## Intro
* We will perform a very simple analysis, just to understand how it works in LLVM.
* The program that will be fed to our LLVM pass will have a function that performs additions.
* Take a look at one possible content of such function:
```llvm
%a = add i32 1, 2
%b = add i32 3, 4
%c = add i32 %a, %b
```
* The first two instructions presented in code above are called __constant on instructions. This means that all of its operands are constants.__
* As you might have already guessed, we could have already optimized the code shown above by using the __constant propagation optimization.__
* However, for now, we will just analyze this function in order to collect information about the __instructions that have only constants as their operands.__