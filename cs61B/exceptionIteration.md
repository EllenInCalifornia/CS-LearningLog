# implicit Exception 
thrown by java 
# explicit Exception
more descriptive 
```java
public V get(K key) {
   int location = findKey(key);
   if (location < 0) {throw new IllegalArgumentException("Key " + 
                            key + " does not exist in map.");  }
   return values[findKey(key)];
}
```

# Handling Errors

<img width="996" alt="image" src="https://user-images.githubusercontent.com/118059669/218244487-aa50aa6a-6cd9-4392-bc3b-34f24cb87269.png">

# RuntimeException API
<img width="968" alt="image" src="https://user-images.githubusercontent.com/118059669/218244521-cc916a39-d663-4b1f-b9a5-59dbf5a8163a.png">



