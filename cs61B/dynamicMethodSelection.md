# Static and Dynamic Type, Dynamic Method Selection
* Every variable in Java has a “compile-time type”, a.k.a. “static type”.
* * This is the type specified at declaration. Never changes!

* Variables also have a “run-time type”, a.k.a. “dynamic type”.
* * This is the type specified at instantiation (e.g. when using new).
* * Equal to the type of the object being pointed at.

## Dynamic Method Selection For Overridden Methods
* Suppose we call a method of an object using a variable with:
* * compile-time type X
* * run-time type Y
* Then if Y overrides the method, Y’s method is used instead. 
* This is known as “dynamic method selection”

### Example 区分 overload vs override 
* Dynamic method selection plays no role when it comes to overloaded methods.
```java 
public interface Animal {
  default void greet(Animal a) {
    print("hello animal"); }
  default void sniff(Animal a) {
    print("sniff animal"); }
  default void flatter(Animal a) {
    print("u r cool animal"); }
}
```
```java 
public class Dog implements Animal {
  void sniff(Animal a) {
    print("dog sniff animal"); }
  void flatter(Dog a) {
    print("u r cool dog"); }
```
```java 
Animal a = new Dog();
Dog d = new Dog();
a.greet(d);   // "hello animal"
a.sniff(d);   // "dog sniff animal"
d.flatter(d); // "u r cool dog"
a.flatter(d); // “u r cool animal” （flatter is overloaded, not overridden!）
```




# interface inheritance: make code general 
* interface is a specification of what a class is able to do, not how to do it. 
* keyword implements: tell the Java compiler that SLList and AList are hyponyms of List61B
```java
public class AList<T> implements List61B<T> { }
```
## method overriding Vs overloading 
| overriding | overloading |
|------------|-------------|
|if a subclass has a method with the exact same signature as<br>in the superclass, we say the subclass overrides the method | 不限于inheritance， same name but different signatures|

<img width="1021" alt="image" src="https://user-images.githubusercontent.com/118059669/216485490-67b4613c-0cb3-4cdb-bcb6-583d11d19c59.png">

* method overloading: same name but different signatures 
```java
public static String longest(AList<String> list) {
    ...
}

public static String longest(SLList<String> list) {
    …
}
```
* @Override Annotation 
* * 1） Main reason: Protects against typos.
* * 2） Reminds programmer that method definition came from somewhere higher up in the inheritance hierarchy.
## interface inheritance 
* specifying the capabilities of a subclass using the implements keyword
* interface: the list of all method signatures
* subclasses must override all of these methods
* if X is a superclass of Y, then memory boxes for x may contain y, 反之不行

## implementation inheritance
* Use the default keyword to specify a method that subclasses should inherit from an interface.
```java 
public interface List61B<Item> {
   public void addFirst(Item x);
   public void addLast(Item y);
   public Item getFirst();
   public Item getLast();
   public Item removeLast();
   public Item get(int i);
   public void insert(Item x, int position);
   public int size();  
   default public void print() {
      for (int i = 0; i < size(); i += 1) {
         System.out.print(get(i) + " ");
      }
      System.out.println();
   }
}
```
## overriding default methods 
* 即使superclass里有这个method， subclass 仍然可以忽略这个default，重写这个method， override 
If you don’t like a default method, you can override it. Any callwill use this method instead of default.


