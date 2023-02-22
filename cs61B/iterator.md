# how the for loop works 
* The code on the left is just shorthand for the code on the right. 
<img width="774" alt="image" src="https://user-images.githubusercontent.com/118059669/220510284-b4ff9442-ab53-4be1-ad98-fa6845a85219.png">
## 右边代码运行的前提
1） friends implements List interface, so list should have iterator method that return an iterator
2)  the iterator method should return an iterator 
3)  seer is an iterator, so iterator should have hasNext and next method 
## 具体实现
1） The List interface extends the Iterable Interface, inheriting the abstract iterator() method 
备注： A class can extend a class and can implement any number of interfaces simultaneously.
<img width="696" alt="image" src="https://user-images.githubusercontent.com/118059669/220513499-28b7ce02-ca7e-4295-a9ab-882b1314ec65.png">

2) 
