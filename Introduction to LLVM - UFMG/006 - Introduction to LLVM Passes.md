# 006 - Introduction to LLVM Passes

## Intro
* LLVM passes are performed in the Middle-End of a compiler.
* __Also, they are the primary tool that a compiler uses to optimize code.__
* In LLVM, as we have previously seen, the tool that executes the LLVM passes is the ```opt``` tool.
* There are 2 types of passes:
  * __Transformation Pass:__ Responsible for modifying the code in some way, that the output is a new version of the code but preserving its semantics, while making it faster, or shorter, or having some useful property.
  * __Analysis Pass:__ Responsible for not modifying the code. Instead, it emits different types of information that make the job of subsequent passes easier.

## Types of Passes
### Intro
* There are different types of passes. Each one of them deals with a different scope.

### The Types
* __Loop Pass:__ It analyzes of modifies loops.
* __Function Pass:__ It is one level up, regarding scope, compared to the loop pass. This type of pass runs on individual functions of the program. 
* __Module Pass:__ It is one level up, regarding scope, compared to the function pass. This type of pass runs on a whole module at a time.
* Other types of passes include: __Call-Graph SCC Pass, Region Pass, Machine Function Pass.__

## Analysis Passes
### Analysis Examples
* __Range Analysis:__ This analysis is responsible for identifying the range of values that a variable may assume.
* __Scalar Evolution:__ This analysis is responsible for identifying how variables inside a loop evolve through the loop iterations.
* __Dominator Tree:__ As we've seen, the Dominator Tree is a very useful data-structure in the context of Compilers courses. This data structure is responsible for telling us which part of the code will for sure run before some other part of the code.

## Transformation Passes
### Transformation Examples
* __Dead Code Elimination:__ This transformation is used to remove parts of code from our program source code that will never be executed.
```c
if(1 < 2){
  v = 4;
}else{
  v = 5;
}
// Since 1 < 2 is always true. We can remove this if-else statement and just put the following line of code:

v = 4;
```
* __Constant Propagation:__  This transformation is responsible for replacing variables with their known constant values to simplify expressions and reduce runtime computations.
```c
int a = 10; // "a" always has the value 10
int b = a + 20; // Thus, "b" = "a" + 20 = 10 + 20 = 30
int c = b * 5 // Finally, "c" = "b" * 5 = 30 * 5 = 150

// The code above can be easily transformed into the code below by applying the constant propagation optimization:

int a = 10;
int b = 30;
int c = 150;
```
* __Loop Invariant Code Motion:__ This transformation is responsible for identifying computations within a loop that produce the same result in every iteration of the loop. After this, such computations are removed from within the loop and put outside of it (and also before the loop).
```c
int sum = 0;
for(int i = 0; i < size; i++){
  int x = size * 2; // Pay attention to the fact that the value of 'x' does not change through the loop
  int sum = i * size;
}

// Thus, the code above can be optimized/transformed into the code below:

int sum = 0;
int x = size * 2;
for(int i = 0; i < size; i++){
  int sum = i * size;
}
```
