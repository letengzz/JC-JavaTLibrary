# Java注解(`Annotation`)简介

从 Java 5 版本之后可以在源代码中嵌入一些补充信息，这种补充信息称为**注解**(`Annotation`)，是 Java 平台中非常重要的一部分。注解都是 `@` 符号开头的。**注解也属于一种类型**。

未来的开发模式都是基于注解的，JPA是基于注解的，Spring2.5以上都是基于注解的，Hibernate3.x以后也是基于注解的，现在的Struts2有一部分也是基于注解的了，注解是一种趋势，一定程度上可以说：**框架 = 注解 + 反射 + 设计模式**。

> Annotation 可以翻译为“注解”或“注释”，一般翻译为“注解”，因为“注释”一词已经用于说明“//”、“/**...*/”和“/*...*/”等符号了，这里的“注释”是英文 Comment 翻译。

**说明**：

- **注解并不能改变程序的运行结果**，也不会影响程序运行的性能。有些注解可以在编译时给用户提示或警告，有的注解可以在运行时读写字节码文件信息。

- 注释会被编译器直接忽略，注解则可以被编译器打包进入class文件，因此，注解是一种用作标注的"**元数据**"(一种描述数据的数据)。

- 从JVM的角度看，注解本身对代码逻辑没有任何影响，如何使用注解完全由工具决定。

- Annotation 可以像修饰符一样被使用，可用于修饰包、类、构造器、方法、成员变量、参数、局部变量的声明，这些信息被保存在Annotation 的 "`name=value`"中。

**例**：

```java
@Override
public String toString() {
  return "Hello";
}
```

上面的代码重写了 `Object` 类的 `toString()` 方法并使用了 `@Override` 注解。如果不使用 `@Override` 注解标记代码，程序也能够正常执行。那么这么写的好处是，使用 `@Override` 注解就相当于告诉编译器这个方法是一个重写方法，如果父类中不存在该方法，编译器便会报错，提示该方法没有重写父类中的方法。这样可以防止不小心拼写错误造成麻烦。

在没有使用 `@Override` 注解的情况下，将 `toString()` 写成了 `toStrring()`，这时程序依然能编译运行，但运行结果会和所期望的结果大不相同。

# 注解的作用

1. 生成帮助文档。这是最常见的，也是 Java 最早提供的注解。常用的有 `@see`、`@param` 和 `@return` 等。
2. 跟踪代码依赖性，实现替代配置文件功能。比较常见的是 [Spring](../../../JavaEE/Frame/Spring/README.md) 2.5 开始的基于注解配置。作用就是减少配置。现在的框架基本都使用了这种配置来减少配置文件的数量。
3. 在编译时进行格式检查。如把 `@Override` 注解放在方法前，如果这个方法并不是重写了父类方法，则编译时就能检查出。

# 注解的分类

1. 由编译器使用的注解：

   - [`@Override`](Built_in/Basic/Override)：让编译器检查该方法是否正确地实现了覆写。

   - [`@SuppressWarnings`](Built_in/Basic/SuppressWarnings.md)：告诉编译器忽略此处代码产生的警告。

   这类注解不会被编译进入`.class`文件，它们在编译后就被编译器扔掉了。

2. 由工具处理`.class`文件使用的注解，比如有些工具会在加载class的时候，对class做动态修改，实现一些特殊的功能。这类注解会被编译进入`.class`文件，但加载结束后并不会存在于内存中。这类注解只被一些底层库使用，一般我们不必自己处理。

3. 在程序运行期能够读取的注解，它们在加载后一直存在于JVM中，这也是最常用的注解。例如，一个配置了`@PostConstruct`的方法会在调用构造方法后自动被调用（这是Java代码读取该注解实现的功能，JVM并不会识别该注解）。

无论是哪一种注解，本质上都一种数据类型，是一种接口类型。到 Java 8 为止 Java SE 提供了 11 个**内置注解**。其中有 5 个是[基本注解](Built_in/Basic/README.md)，它们来自于 `java.lang` 包。有 6 个是[元注解](Built_in/Meta/README.md)，它们来自于 `java.lang.annotation` 包，[自定义注解](annotation_custom.md)会用到元注解。

**提示**：元注解就是负责注解其他的注解。

**根据注解是否包含成员变量**，可以分为如下两类：

1. **标记注解**：没有定义成员变量的注解类型被称为**标记注解**。这种注解仅利用自身的存在与否来提供信息， `@Override`、`@Test` 等都是标记注解。
2. **元数据注解**：包含成员变量的注解，因为它们可以接受更多的元数据，所以也被称为**元数据注解**。

# 定义注解

注解的成员变量在注解定义中以无参数方法的形式来声明。其方法名和返回值定义 了该成员的名字和类型。我们称为**配置参数**。 

可以在定义 Annotation 的成员变量时为其指定初始值，指定成员变量的初始值可使用 default 关键字； 如果只有一个参数成员，建议使用参数名为value； 如果定义的注解含有配置参数，那么使用时必须指定参数值，除非它有默认值。格式是"`参数名 = 参数值`"，如果只有一个参数成员，且名称为value，可以省略"`value=`"； **没有成员定义的 Annotation 称为标记**；**包含成员变量的 Annotation 称为[元数据注解](Built_in/Meta/README.md)** 

配置参数类型：

- [所有基本类型](../../Basis/Primitive_Types/README.md)
- [String](../Object_Oriented/Class/String/README.md)
- [枚举类型](../../Basis/Reference_Types/Enum/README.md)
- [Class类](../Object_Oriented/Class/README.md)
- [Annotation类型](./README.md)
- 以及以上类型的数组

因为配置参数必须是常量，所以，上述限制保证了注解在定义时就已经确定了每个参数的值。

**注解的配置参数可以有默认值，缺少某个配置参数时将使用默认值**。

大部分注解会有一个名为`value`的配置参数，对此参数赋值，可以只写常量，相当于省略了`value`参数。

**例**：

```java
public class Hello {
    @Check(min=0, max=100, value=55)
    public int n;

    @Check(value=99)
    public int p;

    @Check(99) // @Check(value=99)
    public int x;

    @Check
    public int y;
}
```

`@Check`就是一个注解。第一个`@Check(min=0, max=100, value=55)`明确定义了三个参数，第二个`@Check(value=99)`只定义了一个`value`参数，它实际上和`@Check(99)`是完全一样的。最后一个`@Check`表示所有参数都使用默认值。