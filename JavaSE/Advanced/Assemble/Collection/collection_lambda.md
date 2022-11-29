# 使用Lambda表达式遍历Collection集合

[Java](http://c.biancheng.net/java/) 8 为 Iterable 接口新增了一个 forEach(Consumer action) 默认方法，该方法所需参数的类型是一个函数式接口，而 Iterable 接口是 Collection 接口的父接口，因此 Collection 集合也可直接调用该方法。

当程序调用 Iterable 的 forEach(Consumer action) 遍历集合元素时，程序会依次将集合元素传给 Consumer 的 accept(T t) 方法（该接口中唯一的抽象方法）。正因为 Consumer 是函数式接口，因此可以使用 Lambda 表达式来遍历集合元素。

如下程序示范了使用 Lambda 表达式来遍历集合元素。

```
public class CollectionEach {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add("C语言中文网Java教程");        objs.add("C语言中文网C语言教程");        objs.add("C语言中文网C++教程");        // 调用forEach()方法遍历集合        objs.forEach(obj -> System.out.println("迭代集合元素：" + obj));    }}
```

输出结果为：

迭代集合元素：C语言中文网C++教程
迭代集合元素：C语言中文网C语言教程
迭代集合元素：C语言中文网Java教程

上面程序中粗体字代码调用了 Iterable 的 forEach() 默认方法来遍历集合元素，传给该方法的参数是一个 Lambda 表达式，该 Lambda 表达式的目标类型是 Comsumer。forEach() 方法会自动将集合元素逐个地传给 Lambda 表达式的形参，这样 Lambda 表达式的代码体即可遍历到集合元素了。