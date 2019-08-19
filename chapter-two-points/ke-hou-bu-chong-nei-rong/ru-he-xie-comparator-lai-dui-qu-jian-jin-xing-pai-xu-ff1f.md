## 如何写 Comparator 来对区间进行排序？

对于数组、链表、堆等结构，标准库中排序方法，往往是对于基本类型的升序排序，有的时候，不一定能满足我们的要求。例如我们有一些特殊的顺序要求，或待排序的对象类型不是基本类型。此时，就需用到**自定义排序**。自定义排序可以用在很多地方，比如数组排序，堆的排序规则等。

## 一、Java实现自定义排序

Java实现自定义排序，主要有两种方法：

### 1.实现Comparable接口：

以`Interval`区间为例，在定义该类时，让其实现Comparable，并重写其中的compareTo方法，使得Interval类可以进行大小比较，这样也可实现自定义的排序：

```java
class Interval implements Comparable<Interval> {
    int left, right;
    Interval(int left, int right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int compareTo(Interval o) {
        return this.left - o.left;
    }
}
```

这样，在其他地方就可以直接对Interval对象的大小进行比较。完整的测试方法如下：

```java
import java.util.ArrayList;
import java.util.List;
import static java.util.Collections.sort;

// Interval类如上

public class Main {
    public static void main(String[] args) {
        List<Interval> A = new ArrayList<>();
        A.add(new Interval(1, 7));
        A.add(new Interval(5, 6));
        A.add(new Interval(3, 4));
        System.out.println("Before sort:");
        for (Interval i : A)
            System.out.println("(" + i.left + ", " + i.right + ")");

        sort(A);
        System.out.println("After sort:");
        for (Interval i : A)
            System.out.println("(" + i.left + ", " + i.right + ")");
    }
}
```



