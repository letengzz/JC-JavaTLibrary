# Iterator（迭代器）遍历Collection集合元素

Iterator（迭代器）是一个接口，它的作用就是遍历容器的所有元素，也是 [Java](http://c.biancheng.net/java/) 集合框架的成员，但它与 Collection 和 Map 系列的集合不一样，Collection 和 Map 系列集合主要用于盛装其他对象，而 Iterator 则主要用于遍历（即迭代访问）Collection 集合中的元素。

Iterator 接口隐藏了各种 Collection 实现类的底层细节，向应用程序提供了遍历 Collection 集合元素的统一编程接口。Iterator 接口里定义了如下 4 个方法。

- boolean hasNext()：如果被迭代的集合元素还没有被遍历完，则返回 true。
- Object next()：返回集合里的下一个元素。
- void remove()：删除集合里上一次 next 方法返回的元素。
- void forEachRemaining(Consumer action)：这是 Java 8 为 Iterator 新增的默认方法，该方法可使用 Lambda 表达式来遍历集合元素。


下面程序示范了通过 Iterator 接口来遍历集合元素。

```
import java.util.Collection;import java.util.HashSet;import java.util.Iterator;public class IteratorTest {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add("C语言中文网Java教程");        objs.add("C语言中文网C语言教程");        objs.add("C语言中文网C++教程");        // 调用forEach()方法遍历集合        // 获取books集合对应的迭代器        Iterator it = objs.iterator();        while (it.hasNext()) {            // it.next()方法返回的数据类型是Object类型，因此需要强制类型转换            String obj = (String) it.next();            System.out.println(obj);            if (obj.equals("C语言中文网C语言教程")) {                // 从集合中删除上一次next()方法返回的元素                it.remove();            }            // 对book变量赋值，不会改变集合元素本身            obj = "C语言中文网Python语言教程";        }        System.out.println(objs);    }}
```

从上面代码中可以看出，Iterator 仅用于遍历集合，如果需要创建 Iterator 对象，则必须有一个被迭代的集合。没有集合的 Iterator 没有存在的价值。

注意：Iterator 必须依附于 Collection 对象，若有一个 Iterator 对象，则必然有一个与之关联的 Collection 对象。Iterator 提供了两个方法来迭代访问 Collection 集合里的元素，并可通过 remove() 方法来删除集合中上一次 next() 方法返回的集合元素。

上面程序中第 24 行代码对迭代变量 obj 进行赋值，但当再次输岀 objs 集合时，会看到集合里的元素没有任何改变。所以当使用 Iterator 对集合元素进行迭代时，Iterator 并不是把集合元素本身传给了迭代变量，而是把集合元素的值传给了迭代变量，所以修改迭代变量的值对集合元素本身没有任何影响。

当使用 Iterator 迭代访问 Collection 集合元素时，Collection 集合里的元素不能被改变，只有通过 Iterator 的 remove() 方法删除上一次 next() 方法返回的集合元素才可以，否则将会引发“java.util.ConcurrentModificationException”异常。下面程序示范了这一点。

```
public class IteratorErrorTest {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add("C语言中文网Java教程");        objs.add("C语言中文网C语言教程");        objs.add("C语言中文网C++教程");        // 获取books集合对应的迭代器        Iterator it = objs.iterator();        while (it.hasNext()) {            String obj = (String) it.next();            System.out.println(obj);            if (obj.equals("C语言中文网C++教程")) {                // 使用Iterator迭代过程中，不可修改集合元素，下面代码引发异常                objs.remove(obj);            }        }    }}
```

输出结果为：

C语言中文网C++教程
Exception in thread "main" java.util.ConcurrentModificationException
    at java.util.HashMap$HashIterator.nextNode(Unknown Source)
    at java.util.HashMap$KeyIterator.next(Unknown Source)
    at IteratorErrorTest.main(IteratorErrorTest.java:15)

上面程序中第 15 行代码位于 Iterator 迭代块内，也就是在 Iterator 迭代 Collection 集合过程中修改了 Collection 集合，所以程序将在运行时引发异常。

Iterator 迭代器采用的是快速失败（fail-fast）机制，一旦在迭代过程中检测到该集合已经被修改（通常是程序中的其他线程修改），程序立即引发 ConcurrentModificationException 异常，而不是显示修改后的结果，这样可以避免共享资源而引发的潜在问题。

> 快速失败（fail-fast）机制，是 Java Collection 集合中的一种错误检测机制。

注意：上面程序如果改为删除“C语言中文网C语言教程”字符串，则不会引发异常。这样可能有些读者会“心存侥幸”地想，在迭代时好像也可以删除集合元素啊。实际上这是一种危险的行为。对于 HashSet 以及后面的 ArrayList 等，迭代时删除元素都会导致异常。只有在删除集合中的某个特定元素时才不会抛出异常，这是由集合类的实现代码决定的，程序员不应该这么做。