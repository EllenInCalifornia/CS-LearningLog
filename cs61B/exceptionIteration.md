
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
## 例子 ： 
* Compiler requires that these be “caught” or “specified”.
* Goal: Disallow compilation to prevent avoidable program crashes.
<img width="878" alt="image" src="https://user-images.githubusercontent.com/118059669/219542744-5c17412a-e250-414c-89c3-5100a40270e2.png">

## unchecked exceptions will compile just fine (but will crash at runtime).

# checked vs unchecked exceptions 
* Any subclass of RuntimeException or Error is unchecked, all other Throwables are checked.
<img width="838" alt="image" src="https://user-images.githubusercontent.com/118059669/219543243-7a0bc17b-ec5a-4050-b0c7-e6ef69122661.png">

## 处理checked expections 
* Compiler requires that all checked exceptions be **caught or specified**.
# 第1种方法 - catch 
<img width="660" alt="image" src="https://user-images.githubusercontent.com/118059669/219544334-5a3206e2-c3f6-4540-aba5-787acde292ad.png">
* 注意 IOException 属于 exception 
# 第2种方法 - specify
<img width="889" alt="image" src="https://user-images.githubusercontent.com/118059669/219544742-98ef937c-68c3-4251-808b-ee90fe84890d.png">

## 需要注意： If a method uses a ‘dangerous’ method (i.e. might throw a checked exception), it becomes dangerous itself.
* 下例中 main method 因为使用了gulgate, 它本身也变成了dangerous method 
<img width="1148" alt="image" src="https://user-images.githubusercontent.com/118059669/219545870-5301beff-a92d-4009-9610-8f94eb3072c0.png">
## 应对方法
<img width="968" alt="image" src="https://user-images.githubusercontent.com/118059669/219545977-d301e345-ac90-4ee2-9a3f-3cbc2c23acad.png">











