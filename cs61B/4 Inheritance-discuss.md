# Extend Error- no default constructor available in superclass 
* about extend, if the subclass does not specify a constructor explicitly (as in B), <br>the Java compiler will create a parameterless constructor, That's trying to call the superclass parameterless constructor - so it has to exist.
* if the superclass doesn't have a parameterless constructor, the subclass will not be compilable 
* 
