# static 
* can apply the static keyword to variables, methods, blocks, and nested classes
* means that the particular member belongs to a type itself, rather than to an instance of that type.
## static Field 
* public static int numberOfCars;
## The static Methods (Or Class Methods)
### non- static method 下自动生成一个instance: this，can access 本class的<br>static/non- static variables
* We also commonly** use static methods to create utility or helper classes** so that we can<br> get them without creating a new object of these classes.
* static methods in Java are resolved at compile time. Since method overriding is part of <br>Runtime Polymorphism,
* * static methods can't be overridden.
* * Abstract methods can't be static.
* * static methods can't use this or super keywords.

* The following combinations of the instance, class methods, and variables are valid:
* * instance methods can directly access both instance methods and instance variables
* * instance methods can also access static variables and static methods directly
* * static methods can access all static variables and other static methods
* * static methods can't access instance variables and instance methods directly. <br>They need some object reference to do so.
## Class
* top-level class and nested classes 
* In the Java programming language, you can not make a top-level class static.
### nested class
* A nested class has access to the members, including private members, <br>of the class in which it is nested. But the enclosing class does<br> not have access to the members
of the nested class.
#### static nested class
* static nested classes can access all static members of the enclosing class
* In fact, static nested classes behave exactly like any other top-level class, <br>but are enclosed in the only class that will access it, to provide better packaging convenience.
* Basically, a static nested class doesn't have access to any instance members<br> of the enclosing outer class. It can only access them through an object's reference.

####  Non-static nested classes(inner classes)
* inner classes have access to all members of the enclosing class (including private ones), whereas the static nested classes only have access to <br>static members of the outer class.


# compile error: non static variable cannot be referenced from a static context 
# main() method is a static method， 
*The error non static variable cannot be referenced from a static context in Java: The reason to occur this error is that they use a non-static member variable in the main() method. 
# main() method is a static nested method, so it does not have access to other members of the enclosing class;
# 1 
<img width="563" alt="image" src="https://user-images.githubusercontent.com/118059669/217159583-d5f72420-1ef0-483d-b29f-c96715b26b4c.png">

## problem1: how does a nested static class access other members of the enclosing class


* Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private. Static nested classes do not have access to other members of the enclosing class. 
# A nested class is a member of its enclosing class.
## access a nested non- static class from another class 
```java 
public class DMSList {
    private IntNode sentinel;
    public DMSList() {
        //错： expression expected
        // sentinel = new IntNode(-100, LastNode);
        sentinel = new IntNode(-100, null);
    }
    public class IntNode {
        public int item;
        public IntNode Next;
        public IntNode(int i, IntNode n) {
            item = i;
            Next = n;
        }
  }
  ```
 ```java 
 public class Error1 {
    public static void main(String[] args) {
        DMSList l = new DMSList();
        System.out.println(l.max());
        DMSList.IntNode k = new IntNode(1,null);
    }
}
```
##  in the above code, IntNode is a non- static method, so it can only be accessed by creating an instance of its outerclass, using the following syntax
```java
   OuterClass outerObject = new OuterClass();
   OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```
## fix to Error1 
```java
public class Error1 {
    public static void main(String[] args) {
        DMSList l = new DMSList();
        System.out.println(l.max());
        DMSList.IntNode k = l.new IntNode(1,null);
    }
}
```
  
