# Defining New Functions
## function definitions
* a powerful abstraction technique by which a name can be bound to compound operation, which can then be referred to as a unit.
```java
def square(x):
        return mul(x, x)
```
* x in this definition is called a formal parameter, which provides a name for the thing to be multiplied. 
* **def** creates this user-defined function and associates it with the **name** square.
* Both def statements and assignment statements bind names to values, and any existing bindings are lost. 

## Environments
* An environment in which an expression is evaluated consists of a sequence of frames, depicted as boxes. Each frame contains bindings, <br> each of which associates a name with its corresponding value. There is a single global frame.

## Aspects of a functional abstraction
* The domain: the set of arguments it can take.
* The range: the set of values it can return.
* The intent: the relationship it computes between inputs and output (as well as any side effects it might generate).

## Operators
* 2 + 3, (2 + 3) * (4 + 5)
* add(2, 3), mul(add(2, 3), add(4, 5))
* normal division / : results in a floating point, or decimal value, even if the divisor evenly divides the dividend:


# control
* python has rules for automatically displaying the value of any expression you type in. 
