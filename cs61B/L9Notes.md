# 9. Extends, Casting, Higher Order Functions 

* Higher Order Function: A function that treats another function as data.
* e.g. takes a function as input.
## example in python 

```python
def tenX(x):
	return 10*x
 
def do_twice(f, x):
	return f(f(x))
 
print(do_twice(tenX, 2))
```
<br/><br/>
但是old java里function 不能当作argument，但是可以用interface
<img width="837" alt="image" src="https://user-images.githubusercontent.com/118059669/216334176-44b34915-4c41-4fe3-ba13-d338cd26cdd4.png">


## example in java 
<img width="898" alt="image" src="https://user-images.githubusercontent.com/118059669/216334352-56490d0c-e23b-4373-b09f-bc7ef4ea2a24.png">
<br/><br/>
<img width="873" alt="image" src="https://user-images.githubusercontent.com/118059669/216336486-3a822ec7-752f-470f-b4f4-29958c15b052.png">

## overide Vs overload 
* if a subclass has a method with the exact same signature as in the superclass, we say the subclass overrides the method
* Java allows multiple methods with same name, but different parameters/signatures. This is called method overloading
<img width="730" alt="image" src="https://user-images.githubusercontent.com/118059669/216481723-151d0228-5978-4760-96f7-d3698d28d0f4.png">

# Extends, Casting

<img width="941" alt="image" src="https://user-images.githubusercontent.com/118059669/216213863-37132c85-a166-4d10-8316-3bfd8e0416d9.png">


## 以下代码有SLList的全部method，同时多了rotateRight 
```java
public class RotatingSLList<Item> extends SLList<Item> {
	/** Rotates list to the right. */
	public void rotateRight() {
	    Item x = removeLast();
	    addFirst(x);
    }
 }
 ```
 
 <img width="845" alt="image" src="https://user-images.githubusercontent.com/118059669/216215247-be6c8578-3b68-48b5-ad17-07216072ae86.png">

## Example- vengefulList
### code1 

```java
/** SList with additional operation printLostItems() which prints all items
  * that have ever been deleted. */
public class VengefulSLList<Item> extends SLList<Item> {
    private SLList<Item> deletedItems;
    @Override
    public Item removeLast() {
        Item x = super.removeLast();
        deletedItems.addLast(x);
        return x;
    }

    /** Prints deleted items. */
    public void printLostItems() {
        deletedItems.print();
    }
}
```
备注：    
1） This code doesn't work, because problems deletedItems is uninitialized;  
2) 使用super keyword，copy the superclass's method  
   不能直接粘贴原代码过来: a subclass doesn't have access to private members of its superclass.  

### fix1

```java 
public class VengefulSLList<Item> extends SLList<Item> {
    private SLList<Item> deletedItems;
    public VengefulSLList(Item x) {
        deletedItems = new SLList<Item>();
    }
```
  
备注：    
1） deletedItems is an instance variable(attribute) of VengefulSLList;     
2) 添加了constructor，initialize deletedItems.  

### fix2 initialize when declared
```java
public class VengefulSLList<Item> extends SLList<Item> {
    private SLList<Item> deletedItems = new SLList<Item>();  
```
  
## constructor 
<img width="970" alt="image" src="https://user-images.githubusercontent.com/118059669/216220912-5209825d-eae0-485e-a0fc-13240cce01e4.png">

## constructor with arguments
<img width="967" alt="image" src="https://user-images.githubusercontent.com/118059669/216221712-afe005f0-a187-487d-b1dd-71239ebdc19a.png">

备注：  
if there is no argument in super(), it will call the default constructor with no argument;

## As it happens, every type in Java is a descendant of the Object class.
 VengefulSLList extends SLList.  
 SLList extends Object (implicitly).  

## Modules and encapsulation 
### Module: 
1) A set of methods that work together as a whole to perform some task or set of related tasks.  
2) A module is said to be encapsulated if its implementation is completely hidden, and it can be accessed only through a documented interface.
3) Instance variables private. Methods like resize private.  
4) As we’ll see: Implementation inheritance (e.g. extends) breaks encapsulation!  


<img width="896" alt="image" src="https://user-images.githubusercontent.com/118059669/216233390-6e5ce4e3-7577-4251-a304-c9253b67cf0c.png">
    
    
## Type Checking and Casting

<img width="890" alt="image" src="https://user-images.githubusercontent.com/118059669/216234836-d6de16ca-7466-41e0-aa8d-2f1a53f6b9fc.png">
注意 sl的static Type 是SLList，但是dynamic type 是vengefulSLList.  

<br/><br/>
    
| static type      |   dynamic type |
| ------------------|-------------- |
| compile-time type| run-time type  |

| 注意 |
|-----|
|  If overridden, decide which method to call based on run-time type of variable. |
| Compiler allows method calls based on compile-time type of variable.  |
    
<img width="1047" alt="image" src="https://user-images.githubusercontent.com/118059669/216318036-f462870b-5204-45b8-a68b-1c2d68e21927.png">
<br/><br/>

<img width="841" alt="image" src="https://user-images.githubusercontent.com/118059669/216318971-bf6c966f-0303-4c9e-9891-544316fbe49d.png">

<br/><br/>
小的可以放大的盒子里，但是大的不能放小的盒子里。 supperclass =   new subclass
<img width="874" alt="image" src="https://user-images.githubusercontent.com/118059669/216328948-138250bb-7211-4846-a462-9786159640ea.png">

# casting
<img width="874" alt="image" src="https://user-images.githubusercontent.com/118059669/216329649-f561597a-cec1-4eb7-ad3e-17926be9d2c0.png">

Casting is a powerful but dangerous tool.
* Tells Java to treat an expression as having a different compile-time type.
* In example below, effectively tells the compiler to ignore its type checking duties.

```java 
Poodle frank  = new Poodle("Frank", 5);
Malamute frankSr = new Malamute("Frank Sr.", 100);

Poodle largerPoodle = (Poodle) maxDog(frank, frankSr);
```
if we run the code above, we get a ClassCastException at runtime.







