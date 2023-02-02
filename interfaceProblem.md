### superclass/hypernym
```java
public interface CharacterComparator {
    boolean equalChars(char x, char y);
}
```

### 2 subclasses 
OffByOne里没有constructor，估计是default 有一个constructor 
```java
public class OffByOne implements CharacterComparator {
    @Override
    public boolean equalChars(char x, char y) {
        if (x == y + 1 || x == y - 1) {
            return true;
        }
        return false;
    }
}
```

```java
public class OffByN implements CharacterComparator {
    private int n;

    public OffByN(int a) {
        n = a;
    }
    @Override
    public boolean equalChars(char x, char y) {
        if (x - y == n || y - x == n) {
            return true;
        }
        return false;
    }
}
```

### Palindrome class 里的method 传入了一个CharacterComparator object，之前没见过；

```java
  private boolean isPalindromeHelper(Deque<Character> wd, CharacterComparator cc) {
        if (wd.size() == 0 || wd.size() == 1) {
            return true;
        }
        char f = wd.removeFirst();
        char l = wd.removeLast();
        return cc.equalChars(f, l) && isPalindromeHelper(wd, cc);
    }

    public boolean isPalindrome(String word, CharacterComparator cc) {
        Deque<Character> wd = wordToDeque(word);
        return isPalindromeHelper(wd, cc);
    }
```

### Test中使用时：

```java 
@Test
    public void testisOffbyOnePalindrome() {
        String a = "";
        CharacterComparator cc = new OffByOne();
        assertTrue(palindrome.isPalindrome(a, cc));
        String b = "beautiful";
        assertFalse(palindrome.isPalindrome(b, cc));
        String c = "benda";
        assertTrue(palindrome.isPalindrome(c, cc));
        String d = " ";
        assertTrue(palindrome.isPalindrome(d, cc));
        String e = "a";
        assertTrue(palindrome.isPalindrome(e, cc));

    }
```

```java 
 @Test
    public void testisOffbyNPalindrome() {
        String a = "";
        CharacterComparator cc = new OffByN(3);
        assertTrue(palindrome.isPalindrome(a, cc));
        String b = "abed";
        assertTrue(palindrome.isPalindrome(b, cc));
        String c = "bccb";
        assertFalse(palindrome.isPalindrome(c, cc));
        String d = " ";
        assertTrue(palindrome.isPalindrome(d, cc));
        String e = "a";
        assertTrue(palindrome.isPalindrome(e, cc));

    }
```



  
  
