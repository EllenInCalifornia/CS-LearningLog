# goal:  Create a class ArrayMap
<img width="958" alt="image" src="https://user-images.githubusercontent.com/118059669/217709780-b6ec4fb3-88e7-4159-b7ca-9967561218c5.png">
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
## goal： Create a class MapHelper with two methods:
* 注意 class MapHelper 与 ArrayMap的不同，使用ArrayMap<K,V> 时会create an instance， 但是MapHelper的作用只是提供一个method，所以MapHelper class里的method是static method
* 
