# lead - in
## statements and expressions
* Python code consists of expressions and statements. Broadly, computer programs consist of instructions to either
* * Compute some value - expressions 
* * Carry out some action - statements: not evaluated but executed, they do not produce a value but make some change
## functions (abstraction: bind names to expressions)
* Functions encapsulate logic that manipulates data. urlopen is a function. 
## Objects
* An object seamlessly bundles together data and the logic that manipulates that data, in a way that manages the complexity of both.
## Interpreters
* Evaluating compound expressions requires a precise procedure that interprets code in a predictable way. A program that implements such a procedure, evaluating compound expressions, is called an interpreter. The interpreter endows meaning to the programming language

# 1.2   Elements of Programming
## lead-in
When we describe a language, we should pay particular attention to the means that the language <br>
provides for combining simple ideas to form more complex ideas. Every powerful language has three <br>
such mechanisms:
* primitive expressions and statements, which represent the simplest building blocks that the language provides,
* means of combination, by which compound elements are built from simpler ones, and
* means of abstraction, by which compound elements can be named and manipulated as units
## names  (called varibles in python)
* three ways to bind names to the value 
* * the assignment statement (simplest means of **abstraction**)
* * names are also bound via import statements : from math import pi 
* * names can be bound to functions, eg. max , user- defined functions: def 

## Environment
* The possibility of binding names to values and later retrieving those values by name means that the <br> nterpreter must maintain some sort of memory that keeps track of the names, values, and bindings. <br>This memory is called an environment.
* Environments provide the context in which evaluation takes place, which plays an important role in our understanding of program execution.

## Evaluating Nested Expressions
* primitive cases 
* * A numeral evaluates to the number it names,
* * A name evaluates to the value associated with that name in the current environment.
## the Non-Pure Print Function
* Pure functions. 
* * Functions have some input (their arguments) and return some output (the result of applying them). 
* * applying them has no effects beyond returning a value.
* * a pure function must always return the same value when called twice with the same arguments.
* Non-pure functions.
* * In addition to returning a value, applying a non-pure function can generate side effects, which make some change to the state of the interpreter or computer. A common side effect is to generate additional output beyond the return value, using the print function.
```python3
print(print(1),print(2))
# 1 2 None None 
```
# Functions 
## Calling User-Defined Functions 
* procedure for calling functions:
1) add a local frame, forming a new environment;  
2) bind the function's formal parameters to its arguments in that frame
3) Execute the body of the function in that new environment

## Function signature 
* A function’s signature has all the information needed to create a local frame
<img width="550" alt="image" src="https://user-images.githubusercontent.com/118059669/216764265-4c3d9381-05b1-4424-beed-b48029374e18.png">

## Looking Up Names In Environments
* Every expression is evaluated in the context of an environment.
* So far, the current environment is either:
* * The global framealone, or  
* * A local frame,followed by the global frame.
* An environment is a sequence of frames. 
* A name evaluates to the value bound to that name in the earliest frame of the current environment in which that name is found.

