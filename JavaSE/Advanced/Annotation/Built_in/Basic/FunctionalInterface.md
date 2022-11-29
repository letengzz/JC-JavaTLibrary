# `@FunctionalInterface`注解

在 Lambda 表达式时，我们提到如果接口中只有一个抽象方法（可以包含多个默认方法或多个 static 方法），那么该接口就是函数式接口。`@FunctionalInterface` 就是用来指定某个接口必须是[函数式接口](../../../Functional_Programming/README.md)，所以 `@FunInterface` 只能修饰接口，不能修饰其它程序元素。

> 函数式接口就是为 Java 8 的 Lambda 表达式准备的，Java 8 允许使用 Lambda 表达式创建函数式接口的实例，因此 Java 8 专门增加了 `@FunctionalInterface`。

例如，如下程序使用 `@FunctionalInterface` 修饰了函数式接口：

```java
@FunctionalInterface
public interface FunInterface {
    static void print() {
        System.out.println("你好");
    }

    default void show() {
        System.out.println("我正在学习Java教程");
    }

    void test(); // 只定义一个抽象方法
}
```

编译上面程序，可能丝毫看不出程序中的 `@FunctionalInterface` 有何作用，因为 `@FunctionalInterface` 注解的作用只是告诉编译器检查这个接口，保证该接口只能包含一个抽象方法，否则就会编译出错。

`@FunctionalInterface` 注解主要是帮助程序员避免一些低级错误，例如，在上面的 FunInterface 接口中再增加一个抽象方法 abc()，编译程序时将出现如下错误提示：

```java
"@FunctionInterface"批注无效；FunInterface不是functional接口
```

