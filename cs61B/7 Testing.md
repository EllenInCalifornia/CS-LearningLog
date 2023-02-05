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
## 比较Array
* org.junit.Assert.assertArrayEquals(expected,input);
## 比较String
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

