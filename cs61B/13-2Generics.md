# goal:  Create a class ArrayMap
<img width="958" alt="image" src="https://user-images.githubusercontent.com/118059669/217709780-b6ec4fb3-88e7-4159-b7ca-9967561218c5.png">
## code 
### Map61B 
```java
package Map61B;
import java.util.List;

public interface Map61B<K, V> {
    /* Returns true if this map contains a mapping for the specified key. */
    boolean containsKey(K key);

    /* Returns the value to which the specified key is mapped. No defined
     * behavior if the key doesn't exist (ok to crash). */
    V get(K key);

    /* Returns the number of key-value mappings in this map. */
    int size();

    /* Associates the specified value with the specified key in this map. */
    void put(K key, V value);

    /* Returns a list of the keys in this map. */
    List<K> keys();
}
```
### ArrayMap
```java
package Map61B;

import org.junit.Assert.*;

import java.util.LinkedList;
import java.util.List;
import java.util.ArrayList;
import org.junit.Test;


import static org.junit.Assert.*;

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
        size = 0;
    }

    /** Returns the index of the given key if it exists,
     *  -1 otherwise. */
    private int keyIndex(K key) {
        for (int i = 0; i < size; i++) {
            //if (keys[i] == key)
            // 注意== 是比较的pointer！！！
            if (keys[i].equals(key)) {
                return i;
            }
        }
        return -1;
    }


    public boolean containsKey(K key) {
        //使用自身的method
        int index = keyIndex(key);
        return index > -1;
        // 简化代码，不用写if .., return true; ..false
    }

    public void put(K key, V value) {
        //分情况如果已经存在，则overwrite
        //要用index
        int index = keyIndex(key);

        if (index > -1) {
            values[index] = value;
            //size不变
            return;
        }
            keys[size] = key;
            values[size] = value;
            size++;

        }
    //return value
    public V get(K key) {
        int index = keyIndex(key);
        return values[index];


    }

    public int size() {
        return size;
    }

    public List<K> keys() {
        //List is an abstract data type,
        // it has two implementations
        List<K> ans = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            ans.add(keys[i]);
        }
        return ans;
    }
  ```
    
# ambiguity: two different conversions allowable (implicit type casting)
## Q1
<img width="1004" alt="image" src="https://user-images.githubusercontent.com/118059669/217736586-c95bb333-a338-4b22-8a87-1a2549c54921.png">
* the actual call is: assertEquals(int, Integer)
* answer
 <img width="987" alt="image" src="https://user-images.githubusercontent.com/118059669/217737319-18f43525-846a-48e0-9fcb-7afcf26db5cb.png">

## Q2: 
<img width="1000" alt="image" src="https://user-images.githubusercontent.com/118059669/217737576-ba5ddca2-7ef1-48e4-9de2-fb4ce8fb9431.png">
* answer
* Autobox “expected” into an Integer.
* 解决方法： 
<img width="987" alt="image" src="https://user-images.githubusercontent.com/118059669/217738367-99ebc2bf-5abc-4795-aa05-4cdce7c676c6.png">

# generic methods
## 为什么需要generic methods 
## goal： Create a class MapHelper with two methods:
* get(Map61B, key): Returns the value corresponding to the given key in the map if it exists, otherwise null.
* * Unlike the ArrayMap’s get method, which crashes if the key doesn’t exist.
* maxKey(Map61B): Returns the maximum of all keys in the given ArrayMap. Works only if keys can be compared.

* 注意 class MapHelper 与 ArrayMap的不同，使用ArrayMap<K,V> 时会create an instance， 但是MapHelper的作用只是提供一个method，所以MapHelper class里的method是static method
* get(Map61B, key)应该可以用于任何一个Map61B的object，所以应该是generic，但是此时无法通过generic class来实现
```java
public class MapHelper{
    //generic method
    public static <K, V> V get(Map61B<K, V> map, K key) {
        if (map.containsKey(key)) {
            return map.get(key);
        }
        return null;
    }
}
```


