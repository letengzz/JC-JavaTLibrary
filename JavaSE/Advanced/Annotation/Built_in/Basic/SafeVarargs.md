# `@SafeVarargs`注解

```java
public class HelloWorld {
    public static void main(String[] args) {
        // 传递可变参数，参数是泛型集合
        display(10, 20, 30);
        // 传递可变参数，参数是非泛型集合
        display("10", 20, 30); // 会有编译警告
    }

    public static <T> void display(T... array) {
        for (T arg : array) {
            System.out.println(arg.getClass().getName() + ":" + arg);
        }
    }
}
```

声明了一种可变参数方法 display，display 方法参数个数可以变化，它可以接受不确定数量的相同类型的参数。可以通过在参数类型名后面加入`...`的方式来表示这是可变参数。可变参数方法中的参数类型相同，为此声明参数是需要指定泛型。

但是调用可变参数方法时，应该提供相同类型的参数，代码第 4 行调用时没有警告，而代码第 6 行调用时则会发生警告，这个警告是 unchecked(未检查不安全代码)，就是因为将非泛型变量赋值给泛型变量所发生的。

可用 `@SafeVarargs` 注解抑制编译器警告：

```java
public class HelloWorld {
    public static void main(String[] args) {
        // 传递可变参数，参数是泛型集合
        display(10, 20, 30);
        // 传递可变参数，参数是非泛型集合
        display("10", 20, 30); // 没有@SafeVarargs会有编译警告
    }

    @SafeVarargs
    public static <T> void display(T... array) {
        for (T arg : array) {
            System.out.println(arg.getClass().getName() + "：" + arg);
        }
    }
}
```

上述代码在可变参数 display 前添加了 `@SafeVarargs` 注解，当然也可以使用 `@SuppressWarnings("unchecked")` 注解，但是两者相比较来说 `@SafeVarargs` 注解更适合。

**注意**：`@SafeVarargs`注解不适用于非 static 或非 final 声明的方法，对于未声明为 `static` 或 `final` 的方法，如果要抑制 unchecked 警告，可以使用 [`@SuppressWarnings` 注解](SuppressWarnings.md)。