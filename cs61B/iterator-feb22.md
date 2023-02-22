## The secret of the enhanced for loop 
* The code on the left is just shorthand for the code on the right.
<img width="797" alt="image" src="https://user-images.githubusercontent.com/118059669/220504753-7aaafee1-6317-46d7-be95-cf05aa1f3b13.png">

## for the code to work
* 1) compiler checks that Lists have a method called iterator() that returns an Iterator<Integer>
* 2) then, compiler checks that Iterators have: hasNext() and next() method. 
 
## how to implement 
* 1) The List interface extends the Iterable interface, inheriting the abstract iterator() method
<img width="695" alt="image" src="https://user-images.githubusercontent.com/118059669/220555956-30e709ce-7a26-4d9f-a0da-946bd28d7b48.png">
* 2) The Iterator interface specifies these abstract methods explicitly.
 <img width="745" alt="image" src="https://user-images.githubusercontent.com/118059669/220560032-a2755f77-2ea7-456f-b433-85aefd147550.png">
  

  
  
[image @source](https://www.scaler.com/topics/java/iterable-interface-in-java/)
![image](https://user-images.githubusercontent.com/118059669/220559605-af013f94-b8ec-44a7-afae-6e10160cc5ca.png)

## ArrayMap code (incomplete)
  <img width="803" alt="image" src="https://user-images.githubusercontent.com/118059669/220570928-af3b5162-ebfe-451d-b8e7-fd859266d5fb.png">

  ```java
  /**
 * An array based implementation of the Map61B class.
 */
public class ArrayMap<K, V> implements Map61B<K, V> {

    private K[] keys;
    private V[] values;
    private int size;

    public ArrayMap() {
        keys = (K[]) new Object[100];
        values = (V[]) new Object[100];
    }
  
    /* man-made Iterator(nested class) */
    class KeyIterator {
        private int wizardPosition;

        public KeyIterator() {
            wizardPosition = 0;
        }
        public boolean hasNext() {
            return wizardPosition < size;
        }

        public K next() {
            K returnVal = keys[wizardPosition];
            wizardPosition ++;
            return returnVal;
        }

    }
  ```
                                                                              
  
## in-detail explanation
* 1) the Arraymap class implements Iterable, which has abstract iterator method that calls the iterator interface and returns an iterator
* 2) in the Arraymap class, it overrides the iterator method
* 3) in the arraymap class, there is a non-static nested class(inner class), KeyIterator which implements the Iterator interface

## iterationDemo code
```java 
  public static void main(String[] args) {
        ArrayMap<String, Integer> am = new ArrayMap<String, Integer>();

        am.put("hello", 5);
        am.put("syrups", 10);
        am.put("kingdom", 10);

        ArrayMap.KeyIterator ami = am.new Keyiterator();

        while (ami.hasNext()) {
            System.out.println(ami.next());
        }
    }
}
```

* List implement Iterable interface, which has an abstract iterator method. Then List must override the iterator method. 
* Arraymap has an inner class which implements iterator interface
                                         
## 但是此时还无法用enhanced for loop, 继续优化

* java doesn't know how to instantiate an iterator, 如何解决？

* * 解决方法： add an iterator method 

```java 
  import java.util.Iterator // ( 不用import iterable，但是需要import iterator）
  public Iterator<K> iterator() {
       return new KeyIterator();
  }
```
* 问题： iterator should return an iterator instead of KeyIterator
* * 解决： 
```java 
  
    /* man-made Iterator(nested class) */
   private class KeyIterator implements Iterator <K> { }
```
 这里可以把这个inner class 变成private, 因为public method iterator 仍然让我们可以access this class 
  <br>
  
*  问题：compiler doesn't know that iterator method exists
* * the class must implement iterable 
``` java 
  public class ArrayMap<K, V> implements Map61B<K, V>, Iterable <K> {}
```
## summary 
* in order for the enhance for loop to work, we have to implement iterable 
* for iterable to work, we have to override iterator method
* the inner class must implement iterator interface
                                           
# summary for iteration 
* implement iterable interface to support enhanced for loop 
* iterator() method must return an object that implements the Iterator interface.
## the way to do it without creating an inner class 
```java 
  // we are trying to iterate over keys 
  public Iterator<K> iterator() {
       List<K> keylist = keys();
       return keylist.iterator();
  }
``` 
  
