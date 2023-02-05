# Testing 
## 错误比较 Comparison (==,!=) of reference data types 
* 如果variable是一个reference data type， ==,!= 比较的是存在variable里的address(pointer), <br>只有两个地址完全一样（pointer 指向同一个object）时才满足==; 所以即使内容一样，也不满足==
* Example
```java
String[] input = {"i", "have", "an", "egg"};
String[] expected = {"i", "have", "an", “egg”}; 
//此时 input != expected
```
## ad hoc testing （tedious）
* import java.util.Arrays;
* 使用 if (!Arrays.equals(input, expected))
* 或者逐项对比，使用 input[i].equals(expected[i])

# TDD  Test driven development -使用JUnit
* **比较Array**  
** org.junit.Assert.assertArrayEquals(expected,input);
* **比较String**
*  int cmpr = "abc".compareTo("eft");
* * 备注： 此处提到了deprecated， 一开始用assertEquals在intelliJ里面会高亮，显示deprecated，因为已经有更新版本了
* 先写test
* import org.junit.Test 之后句法变得简单
* * org.junit.Assert.assertArrayEquals(expected,input) 变为 assertEquals(a,expected1);
* * Annotate each test with @Test
* * 这时不需要main
* * 不需要分号
* * 但这是testmethods 不能是static, 因为 JUnit runner 会 instantiate TestXXX.java
 
```java 
import org.junit.Test;
import static org.junit.Assert.*;
public class testSort {
   @Test
    public void testfindSmallest() {
        String[] a = {"i", "abc", "eggs","f"};
        int expected = 2;
        int actual = Sort.findSmallest(a,2);
        assertEquals(expected,actual);
    }
```
# prjGold- autograder 
## Two new ideas
* Randomized testing
* JUnit message generation.
```java
assertEquals("Oh noooo!\nThis is bad:\n   Random number " + actual 
                     + " not equal to " + expected + "!", 
                     expected, actual);
```


## 思路整理
* 测试范围 int 0-1000
* 只assertEquals-remove值
* 用String concatenation 记录log 
* to prevent NullPointerException
* * if size == 0: randomly addFrist，addLast
* * random, 0 or 1 : StdRandom.uniform(2)
* if size != 0: randomly addFrist，addLast, removeFirst, removeLast; 
* * 随机进行4种操作，结合switch
## 回顾
* 耗时3h；
* 学习了random随机的用法，比如一共有几种情况，就用几个随机数；尽量randomize，每次添加的数也进行randomize；
* 复习了switch（x）case 1: 的句法
* 学习了如何用String concatenation 记录failure sequences；
* It is not as difficult as you thought. 

## code 
* 自己没理解题，没想出来 @source flyingpig, [Source Code](https://github.com/PKUFlyingPig/CS61B/blob/e1fc65dcfdcf67e691dd5783f522181026ec0d1e/proj1gold/TestArrayDequeGold.java)

```java
import static org.junit.Assert.*;
import org.junit.Test;
public class TestArrayDequeGold {
    @Test
    public void testStudentArrayDeque() {
        StudentArrayDeque<Integer> testArray = new StudentArrayDeque<>();
        ArrayDequeSolution<Integer> stdArray = new ArrayDequeSolution<>();
        String log = "";
        for (int i = 0; i < 1000; i++) {
            if (testArray.size() == 0) {
                int firstOrLast = StdRandom.uniform(2);
                Integer numberToAdd = StdRandom.uniform(1000);
                if (firstOrLast == 0) {
                    testArray.addFirst(numberToAdd);
                    stdArray.addFirst(numberToAdd);
                    log = log + "addFirst(" + numberToAdd + ")\n";
                } else {
                    testArray.addLast(numberToAdd);
                    stdArray.addLast(numberToAdd);
                    log = log + "addLast(" + numberToAdd + ")\n";
                }
            } else {
                int oneOfFour = StdRandom.uniform(4);
                Integer numberToAdd = StdRandom.uniform(1000);
                Integer removeofTest = 0;
                Integer removeofStd = 0;
                switch (oneOfFour) {
                    case 0:
                        testArray.addFirst(numberToAdd);
                        stdArray.addFirst(numberToAdd);
                        log = log + "addFirst(" + numberToAdd + ")\n";
                        break;
                    case 1:
                        testArray.addLast(numberToAdd);
                        stdArray.addLast(numberToAdd);
                        log = log + "addLast(" + numberToAdd + ")\n";
                        break;
                    case 2:
                        removeofTest = testArray.removeFirst();
                        removeofStd = stdArray.removeFirst();
                        log += "removeFirst()\n";
                        break;
                    case 3:
                        removeofTest = testArray.removeLast();
                        removeofStd = stdArray.removeLast();
                        log += "removeLast()\n";
                        break;

                }
                assertEquals(log, removeofStd, removeofTest);
            }

        }
    }
}
```
