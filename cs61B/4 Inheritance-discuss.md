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

