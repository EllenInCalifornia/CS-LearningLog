# Review: Typing Rules
* Compiler allows the memory box to hold any subtype.
* Compiler allows calls based on static type.
* Overriden non-static methods are selected at runtime based on dynamic type.
* For overloaded methods, the method is selected at compile time.

## exercise 
* casting, 注意外面可以有括号  
```java
Object o2 = new ShowDog("dd",12);
ShowDog sdx = ((ShowDog)o2);
```
# Subtype Polymorphism
* Polymorphism: “providing a single interface to entities of different types”
* Problem：  in python, there is operator overloding, how to do this in Java?
* 术语：callback（回调机制）

## Problematic code 
```java
public class Dog {
    private String name;
    private int size;
    public Dog(String n, int s) {
        name = n;
        size = s;
    }

    public void bark() {
        System.out.println(name + "says: bark");
    }
}
```
```java
public class Maximizer {
    public static Object max(Object[] items) {
        int maxDex = 0;
        for (int i = 0; i < items.length; i++) {
            if (items[maxDex] < items[i]) {
            //problematic 
                maxDex = i;
            }
        }
        return items[maxDex];
    }

    public static void main(String[] args) {
        Dog[] dogs = {new Dog("dd",10), new Dog("ss",15), new Dog("jj",30)};
        Dog maxDog = (Dog) max(dogs);
        maxDog.bark();
    }
}
``` 
* the above code is problematic 

## fix the above code with interface 
* 1) 创建一个interafce OurComparable 
```java 
public interface OurComparable {
    /*returns -1 if this < 0; 0 equal; 1 >;
     */
    public int compareTo(Object o); // Object
}
```
* 2) dogs implements OurComparable, 注意method里的cast type， 把generic type 转成dog 
```java
public class Dog implements OurComparable{
    private String name;
    private int size;
    public Dog(String n, int s) {
        name = n;
        size = s;
    }

    public int compareTo(Object o) {
        //casting the type
        Dog tempDog = (Dog) o;
        if (this.size > tempDog.size) {
            return 1;
        } else if (this.size == tempDog.size) {
            return 0;
        }
        return -1;
    }

    public void bark() {
        System.out.println(name + "says: bark");
    }
}
```
* 3）修改maximizer， main不用修改；<br> OurComparable 代表一个generic class，代表一种 object data type;<br>OurComparable 的一个subclass 是dog 

```java
public class Maximizer {
    public static OurComparable max(OurComparable[] items) {
        int maxDex = 0;
        for (int i = 0; i < items.length; i++) {
            if (items[maxDex].compareTo(items[i]) == -1) {
                maxDex = i;
            }
        }
        return items[maxDex];
    }

    public static void main(String[] args) {
        Dog[] dogs = {new Dog("dd",10), new Dog("ss",15), new Dog("jj",30)};
        Dog maxDog = (Dog) max(dogs);
        maxDog.bark();
    }
}
``` 
now this code works fine. 

## better the above code 
* OurComparable
```java
public interface OurComparable {
    /*returns negative if this < 0; 0 equal; positive >;
     */
    public int compareTo(Object o); // Object
    //等价于== compareTo（OurComparable o）
}
```
* dog code 
```java 
... 
public int compareTo(Object o) {
        //casting the type
        Dog tempDog = (Dog) o;
        return this.size - tempDog.size;
    }
```
* Maximizer

```java 
public static OurComparable max(OurComparable[] items) {
        int maxDex = 0;
        for (int i = 0; i < items.length; i++) {
            if (items[maxDex].compareTo(items[i]) < 0) {
                maxDex = i;
            }
        }
        return items[maxDex];
    }
```

# The Issues With OurComparable
* Awkward casting to/from Objects.
* we made it up 

# built- in interface comparable 
```java
public interface Comparable<T> {
     public int compareTo(T obj);
} 
```
* this interface is already defined and used by tons of libraries. 
* It uses generics.
* Lots of built in classes implement Comparable (e.g. String)
* Lots of libraries use the Comparable interface (e.g. Arrays.sort)
Avoids need for casts.
* if a class implements Comparable<T>, then it has the compareTo method, 比如String

### code using built- in comparable interface 

```java
    public class Dog implements Comparable<Dog> {
    private String name;
    private int size;
    public Dog(String n, int s) {
        name = n;
        size = s;
    }

    public int compareTo(Dog adog) {
        return this.size - adog.size;
    }

    public void bark() {
        System.out.println(name + " says: bark");
    }

}
```

## Comparators
* The term “Natural Order” is sometimes used to refer to the ordering implied by a Comparable’s compareTo method.
* 比如dogs 按size大小排序，但是如果我们想用其他指标排序呢，比如name
### solution: create a nested class inside dog that implements a comparator 
* import java.util.Comparator;
 **comparator interface** 
```java
public interface Comparator<T> {
   int compare(T o1, T o2);
   }
```
* create a nested class inside dog that implements a comparator 
* * we don't need to instantiate a dog to get a NameComparator : <br>it doesn't use instance variable, so we make it static

 ```java
    import java.util.Comparator;

public class Dog implements Comparable<Dog> {
    private String name;
    private int size;
    public Dog(String n, int s) {
        name = n;
        size = s;
    }

    public int compareTo(Dog adog) {
        return this.size - adog.size;
    }
    
    public static class NameComparator implements Comparator<Dog> {
        public int compare(Dog a, Dog b) {
            return a.name.compareTo(b.name);
        }
    }
    public void bark() {
        System.out.println(name + " says: bark");
    }
}

 ```
 * use the NameComparator 
 ```java 
     public static void main(String[] args) {
        Dog[] dogs = {new Dog("dd",10), new Dog("ss",15), new Dog("zz",30)};
        //create an object which can compare dog names
        //nc has the compare method 
        Dog.NameComparator nc = new Dog.NameComparator();
        int firstOrder = 0;
        for (int i = 0; i < dogs.length; i++) {
            if (nc.compare(dogs[firstOrder],dogs[i]) < 0) {
                firstOrder = i;
            }
        }
        dogs[firstOrder].bark();
    }
   ```
### 进一步改进代码，real life中的写法
 * 把nested class 设为private 
 * 写个static method return NameComparator； 
 ```java 
    private static class NameComparator implements Comparator<Dog> {
        public int compare(Dog a, Dog b) {
            return a.name.compareTo(b.name);
        }
    }

    public static Comparator<Dog> getnameComparator() {
        return new NameComparator();
    ```
  使用代码
  ```java 
     Comparator<Dog> nc = Dog.getnameComparator();
    ```

 
## 补充 nested class 
* Nested classes are divided into two categories: static and non-static. <br>Nested classes that are declared static are simply called <br>static nested classes. Non-static nested classes are called inner classes.
### static neste class
* Static nested classes are accessed using the enclosing class name:  
```java 
    OuterClass.StaticNestedClass
```
* create an object for the static nested class  
```java 
 OuterClass.StaticNestedClass nestedObject = new OuterClass.StaticNestedClass();
```
### Non-static neste class (inner class)
  
  * To instantiate an inner class, you must first instantiate the outer class. <br>
    Then, create the inner object within the outer object;
  * An instance of InnerClass has direct access to the methods and fields<br>
    of its enclosing instance.
 ```java 
 OuterClass outerObject = new OuterClass()
 OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```
## 补充 callback
* In C and C++ programming language, the process of calling a function from another<br> 
    function is referred to as callback. The function's memory address is represented<br>
    as the function pointer. In C and C++ languages, we achieve the callback bypassing <br>
    the function pointer to another function.
 * Unlike C and C++ language, Java doesn't have the concept of the callback function. <br>
    Java doesn't use the concept of the pointer, due to which callback functions are not <br>
    supported. However, we can create a callback function by passing an interface that <br>
    refers to the location of the function instead of passing the function's memory address.
 * Interfaces provide us with the ability to make callbacks:
 * * Sometimes a function needs the help of another function that might not have been written yet.
 * * The helping function is sometimes called a “callback”. 

