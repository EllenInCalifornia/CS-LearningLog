https://img-blog.csdnimg.cn/img_convert/0b9fb415f8e99cb24042ba7f6cd0e940.png![image](https://user-images.githubusercontent.com/118059669/219540497-1c8055b2-2892-4b02-ba5f-69b60e55b1c5.png)

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

## exceptions are just instances of classes 

# catch an expception
## Can ‘catch’ exceptions instead, preventing program from crashing. Use keywords try and catch to break normal flow.
<img width="1001" alt="image" src="https://user-images.githubusercontent.com/118059669/219254430-79ba366c-0731-404f-84ce-b7324f8519f3.png">

# take corrective action in catch block 

<img width="984" alt="image" src="https://user-images.githubusercontent.com/118059669/219259972-87c3c5f1-c70f-45dd-8423-d6a47508fb88.png">

# Exceptions allows you to keep error handling code separate from 'real code'
* 左图是右图的优化
<img width="994" alt="image" src="https://user-images.githubusercontent.com/118059669/219260538-6fde32b7-a3f2-446f-967f-8fb42ac48ad8.png">

# Uncaught exceptions: exceptions and the Call Stack 
<img width="1087" alt="image" src="https://user-images.githubusercontent.com/118059669/219261135-807ba745-b3b6-4a01-9d21-595d4ec4f106.png">

# checked exceptions: “Must be Caught or Declared to be Thrown”
* checked and unchecked 是对于javac来说的，也就是编译异常和非编译异常


