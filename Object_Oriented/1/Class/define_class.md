# 定义class

因为Java是面向对象的语言，一个程序的基本单位就是`class`，`class`是关键字，这里定义的`class`名字就是`Person`：

```java
public class Person { // 类名是Person
    public String name;	//name字段
    public int age;	//age字段
    // ...
} // class定义结束
```

一个`class`可以包含多个字段（`field`），字段用来描述一个类的特征。上面的`Person`类，我们定义了两个字段，一个是`String`类型的字段，命名为`name`，一个是`int`类型的字段，命名为`age`。因此，通过`class`，把一组数据汇集到一个对象上，实现了数据封装。



**注意**：

- `public`是[访问修饰符]()，表示该`class`是公开的，可以被外部访问。

- 不写`public`，也能正确编译，但是这个类将无法从命令行执行。