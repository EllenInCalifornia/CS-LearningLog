#Mar 1- lecture 15 Packages,jar
* packages are just like folders
* jar files are just zip files
* creating a jar file:  intelliJ: file - project structure - artifacts- jar - from module with dependencies- build artifacts 
* 上述过程可以通过一些build systems 来自动完成： 
** Ant Maven Gradle

## Access control- private vs protected 
* only code from a given class can access private members. subclass, same package 都不可以; subclass inherit all the members of the parent class, but doesn't not have access to private members; to give subclass access to members, use protected.

* no modifier = package private 

#Feb 28 
it took me two days to figure out lab5, with little help

## lab 5 
## intelliJ
* open settings, short cut (Cmd + ,) 
* make long lines appear within view: setting- editor -general softwrap
## 2D array 
* The length of a 2D array is the number of rows it has.
* uneven.length = 3; eneven[0].length = 3, eneven[1].length = 2;2   
```java
int[][] uneven =
        { { 1, 9, 4 },
          { 0, 2},
          { 0, 1, 2, 3, 4 } };
```
```java
int[][] world = new int[2][3];
        world[0][1] = 1;
        world[0][2] = 1;
        world[0][0] = 3;
        System.out.println(world.length);
        //2
        System.out.println(world[0].length);
        //3
```
* in BoringWorldDemo.java, world is a 2D array of TETiles, you need to fill each index position with a TETiles, then you can you use the renderFrame method in TERenderer.java to draw it to the screen. In TERenderer.java, int numXTiles = world.length;int numYTiles = world[0].length;, so   

# TERenderer.java
* initialize() method
1） setcanvasSize: width * tile_size, height * tile_size
2) xScale(0,width)

## Pseudo random generation and seeds
```java
import java.util.Random;
public class testR {
    public static void main(String[] args) {
        /*pseudo random generation and seeds
        只要seed一样，每次产生的sequence就一样
         */
        Random random = new Random(30);

        for (int i = 0; i < 5; i++) {
            // bound决定了每次的数都在0-bound之间
           System.out.println(random.nextInt(5));
        }

    }
}
```


#  hw1 Feb 25-27 
```java			
    @Override
    public Iterator<T> iterator() {
        return new BqIterator<T>();
    }

    // implement iterator interface;
    private class BqIterator<T> implements Iterator<T> {
        private int ptr;
        BqIterator() {
            ptr = 0;
        }

        @Override
        public boolean hasNext() {
            return ptr < fillCount;
        }
        public T next() {
           //注意这个generic syntax
            T returnValue = (T) rb[ptr];
            ptr++;
            return returnValue;
        }
    }
```

