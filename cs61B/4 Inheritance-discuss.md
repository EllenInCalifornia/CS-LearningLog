# static 
* can apply the static keyword to variables, methods, blocks, and nested classes
* means that the particular member belongs to a type itself, rather than to an instance of that type.
## static Field 
* public static int numberOfCars;
## The static Methods (Or Class Methods)
* We also commonly** use static methods to create utility or helper classes** so that we can<br> get them without creating a new object of these classes.
* static methods in Java are resolved at compile time. Since method overriding is part of Runtime Polymorphism,
* * static methods can't be overridden.
* * Abstract methods can't be static.
* * static methods can't use this or super keywords.

* The following combinations of the instance, class methods, and variables are valid:
* * instance methods can directly access both instance methods and instance variables
* * instance methods can also access static variables and static methods directly
* * static methods can access all static variables and other static methods
* * static methods can't access instance variables and instance methods directly. <br>They need some object reference to do so.
## A static Class
* The main difference between these two is that the inner classes have access to all members<br> of the enclosing class (including private ones), whereas the static nested classes only have access to <br>static members of the outer class.

* In fact, static nested classes behave exactly like any other top-level class, but are enclosed<br> in the only class that will access it, to provide better packaging convenience.

* Basically, a static nested class doesn't have access to any instance members of the enclosing <br>outer class. It can only access them through an object's reference.

* static nested classes can access all static members of the enclosing class, including private ones.

Java programming specification doesn't allow us to declare the top-level class as static. Only <br>classes within the classes (nested classes) can be made as static.

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
    

# prolems with extend
* \\ public void m4() {System.out.println("Cm4-> " + super.super.x); }} can't do super.super
# exercise
* d has the compile type Dog, which has the method bark(Dog d), c is a Dog, so it is compilable 
* but d has the runtime type Corgi, and Corgi's method overrides Dogs bark(Dog d)
* 所以会运行/* Method C */

```java
public class Dog {
    public void bark(Dog d) { /* Method A */ }

}
public class Corgi extends Dog {
    public void bark(Corgi c) { /* Method B */ }
    @Override
    public void bark(Dog d) { /* Method C */ }
    public void play(Dog d) { /* Method D */ }
    public void play(Corgi c) { /* Method E */ }
}

public static void main(String[] args) {
        Dog d = new Corgi();
        Corgi c = new Corgi();
        d.bark(c);
        }
```






# Extend Error- no default constructor available in superclass 
* about extend, if the subclass does not specify a constructor explicitly (as in B), <br>the Java compiler will create a parameterless constructor, That's trying to call the superclass parameterless constructor - so it has to exist.
### parameterless constructor is the default constructor in the superclass,<br>if the superclass doesn't have a parameterless constructor, no default constructor available

*superclass 
```java
public class Animal {
    protected String name, noise;
    protected int age;
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
        this.noise = "Huh?";
    }

    public String makeNoise() { if (age < 5) {
        return noise.toUpperCase(); } else {
        return noise; }
    }
    public void greet() {
        System.out.println("Animal " + name + " says: " + makeNoise());
    }
    public static void main(String[] args) {
        Animal a = new Animal("a", 10);
        a.greet();

    }
}
```
*subclass
* 
```java
public class Cat extends Animal {
    public Cat(String name, int age) {
       //superclass constructor must be explicitly specified;
        super(name, age);
       //Change the value of the field.
       this.noise = "Meow";
    }

    @Override
    public void greet() {
        System.out.println("Cat " + name + " says: " + makeNoise());
    }
}
```
## compile type Error 
<img width="574" alt="image" src="https://user-images.githubusercontent.com/118059669/217121525-5692756b-fdb3-48f4-977b-6109a6cea77b.png">
<img width="547" alt="image" src="https://user-images.githubusercontent.com/118059669/217121555-be8358e8-bdcd-4b25-88b4-b7cc78e379d8.png">

