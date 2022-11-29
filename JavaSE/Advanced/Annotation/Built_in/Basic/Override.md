# `@Override`注解

Java 中 `@Override` 注解是用来指定[方法重写](../../../Object_Oriented/Method/override.md)的，**只能修饰方法并且只能用于方法重写**，不能修饰其它的元素。它**可以强制一个子类必须重写父类方法或者实现接口的方法**。

**例**：

```java
public class Person {
    private String name = "";
    private int age;
    ...
    @Override
    public String t0String() { //toString()
        return "Person [name=" + name + ", age=" + age + "]";
    }
}
```

重写 Object 类的 `toString()` 方法，该方法使用 `@Override` 注解。如果 `toString()` 不小心写成了 `t0String()`，那么程序会发生编译错误。会有如下的代码提示：

```java
类型为 Person 的方法t0String()必须覆盖或实现超类型方法
```

所以 `@Override` 的作用是告诉编译器检查这个方法，保证父类要包含一个被该方法重写的方法，否则就会编译出错。这样可以帮助程序员避免一些低级错误。

当然如果代码中的方法前面不加 `@Override` 注解，即便是方法编辑错误了，编译器也不会有提示。这时 `Object` 父类的 `toString()` 方法并没有被重写，将会引起程序出现 Bug(缺陷)。