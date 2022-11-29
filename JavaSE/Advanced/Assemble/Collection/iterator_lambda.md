# 使用Lambda表达式遍历Iterator迭代器

[Java](http://c.biancheng.net/java/) 8 为 Iterator 引入了一个 forEachRemaining(Consumer action) 默认方法，该方法所需的 Consumer 参数同样也是函数式接口。当程序调用 Iterator 的 forEachRemaining(Consumer action) 遍历集合元素时，程序会依次将集合元素传给 Consumer 的 accept(T t) 方法（该接口中唯一的抽象方法）。

> java.util.function 中的 Function、Supplier、Consumer、Predicate 和其他函数式接口被广泛用在支持 Lambda 表达式的 API 中。“void accept(T t);”是 Consumer 的核心方法，用来对给定的参数 T 执行定义操作。

如下程序示范了使用 Lambda 表达式来遍历集合元素。

```
public class IteratorEach {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add("C语言中文网Java教程");        objs.add("C语言中文网C语言教程");        objs.add("C语言中文网C++教程");        // 获取objs集合对应的迭代器        Iterator it = objs.iterator();        // 使用Lambda表达式（目标类型是Comsumer）来遍历集合元素        it.forEachRemaining(obj -> System.out.println("迭代集合元素：" + obj));    }}
```

输出结果为：

迭代集合元素：C语言中文网C++教程
迭代集合元素：C语言中文网C语言教程
迭代集合元素：C语言中文网Java教程

上面程序中第 11 行代码调用了 Iterator 的 forEachRemaining() 方法来遍历集合元素，传给该方法的参数是一个 Lambda 表达式，该 Lambda 表达式的目标类型是 Consumer，因此上面代码也可用于遍历集合元素。