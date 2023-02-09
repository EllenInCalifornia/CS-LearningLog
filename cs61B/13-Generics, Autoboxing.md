
# next 3 lectures: build an Array based implementation of a Map
# new syntax
* Syntax1: Autoboxing, promotion, immutability, generics
* Syntax2: Exceptions, Iterables/Iterators
* Syntax3: Access control, equals, other loose ends
* Syntax4 (optional): Wildcards, type upper bounds, covariance (not in the scope of the class).

## lead -in 
* Generics, we use Integer instead of int
```java 
ArrayList<String> L = new ArrayList<String>();
```
## reference types 
* Remember: Java has 8 primitive types. All other types are reference types.
* For each primitive type, there is a corresponding reference type called a wrapper class.
<img width="702" alt="image" src="https://user-images.githubusercontent.com/118059669/217696830-d74dd6cf-c448-49ee-93b2-1addaddf63cf.png">

## Autoboxing (auto-unboxing): 
* Implicit conversions between the wrapper type and the primitive type
* primitive types and wrapper types can be used interchangeably 
## notes
* Arrays are never autoboxed/unboxed, e.g. an Integer[] cannot be used in place of an int[] (or vice versa).
* Autoboxing / unboxing incurs a measurable performance impact!
* Wrapper types use MUCH more memory than primitive types.

# 补充private final 
* You must initialize a final variable once and only once. There are three ways to do that for an instance variable:  
1）in the constructor  
2）in an instance initialization block  
3）when you declare it  
## example 

```java
public class X
{
    private final int a;
    private final int b;
    private final int c = 10;

    {
       b = 20;
    }

    public X(final int val)
    {
        a = val;
    }
}
```
