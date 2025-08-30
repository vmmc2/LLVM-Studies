# 005 - Program Visualization using LLVM

## Intro
* Here, we are going to perform program visualization by using the ```opt``` tool, one of the components generated when we compile the LLVM project.
* In order to find out your version of ```opt```, run the command below in the path ```/llvm-project/build/bin/```
```sh
./opt --version
```
* You should see something similar to the output shown below:
```sh
LLVM (http://llvm.org/):
  LLVM version 21.0.0git
  Optimized build.
  Default target: x86_64-unknown-linux-gnu
  Host CPU: tigerlake
```

## Using ```opt```
* We can use this tool to perform the following actions:
  * Program Visualization
  * Program Analysis
    * What kind of instructions the program contains?
    * How many loops does a specific program have?
    * How many pointers does a specific program have?
    * Does the program have vulnerabilities? If so, what kind of vulnerabilities?
  * Program Transformation
    * Instrumentation
    * Optimization

## Program Visualization
* ```opt``` represents programs in the ```DOT``` format, which is a graph description language.
* This specific representation in a graph format has a very specific name. __It is called Control-Flow Graph (CFG).__
* As any other graph, a Control-Flow Graph is composed of vertices and edges:
  * __Vertices: Are called basic blocks. A basic block is just a sequence of instructions that always execute together.__
  * __Edges: Are responsible for representing possible execution paths in a program.__
* There are many tools available on Linux that can be used to visualize ```DOT``` files, some of them are:
  * ```dot```
  * ```graphviz```
  * ```neato```
  * ```twopi```
  * ```circo```
  * ```fdp```
  * ```sfdp```
* __The preferred and recommended ones are ```dot``` and ```graphviz```.__

## Program Regions
* This is another way of performing program visualization, different than a Control-Flow Graph, though.
* In this representation, the basic blocks of the CFG are grouped together in regions. A region is a subgraph of the control-flow graph and it has only one entry point and only one exit point.
* __Side Note: After watching the lesson related to this subject, I am under the impression that the concept of a program region is a little more complex than this.__
* One can see the program visualization based on the concept of Program Regions by executing the following command:
```sh
opt -dot-cfg-only file.ll
```
* If you don't want to see the instructions present in each basic block, in order to get a clearer view of the program regions, you can execute the following command:
```sh
opt -dot-regions-only file.ll
```
* __By analizing the program regions and its structure with the source code of the program, one can easily find correspondences between them.__
* __Side Note: To compute program regions, it is necessary to use a data structure called Dominator Tree.__
* You can see the Dominator Tree responsible for generating the CFG with Program Regions by executing the command shown below:
```sh
opt -dot-dom file.ll
```
* If you don't want to see the instructions present in each basic block, in order to get a clearer view of the Dominator Tree, you can execute the following command:
```sh
opt -dot-dom-only file.ll
```
* An excellent paper about this is __"The Program Dependence Graph and Its Use in Optimization." by Jeanne Ferrante.__
* There are other ways of performing program visualization with ```opt```. To check out which are available in your version of LLVM, you can execute the following command:
```sh
opt --help | grep dot
```
* In my case, I got the following types of visualization:
```sh
--dot-callgraph                                                      - Print call graph to 'dot' file
--dot-dom                                                            - Print dominance tree of function to 'dot' file
--dot-dom-only                                                       - Print dominance tree of function to 'dot' file (with no function bodies)
--dot-postdom                                                        - Print postdominance tree of function to 'dot' file
--dot-postdom-only                                                   - Print postdominance tree of function to 'dot' file (with no function bodies)
--dot-regions                                                        - Print regions of function to 'dot' file
--dot-regions-only                                                   - Print regions of function to 'dot' file (with no function bodies)
--dot-cfg-mssa=<file name for generated dot file>                    - file name for generated dot file
--pgo-view-block-coverage-graph                                      - Create a dot file of CFGs with block coverage inference information
```

## Call Graph
* It is also a graph representation of a program.
* In this representation, the vertices represent functions and the edges represent relationships between callers and callees (both of which are functions). The one who makes the call is named caller, while the one that is called is named callee.
* It can also deal with recursive functions.
* In order to generate the Call Graph of a program, you can execute the command below:
```sh
opt -dot-callgraph file.ll
```
