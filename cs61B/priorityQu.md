# new syntax 没学过
```java
PriorityQueue<String> pqu = new PriorityQueue<>(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return counts.get(o2) - counts.get(o1);
            }
        });
```
