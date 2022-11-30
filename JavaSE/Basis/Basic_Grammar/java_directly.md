# Java直接量(字面量)

**直接量**是指在程序中通过源代码直接给出的值，例如在`int a = 5;`代码中，为变量 a 所分配的初始值 5 就是一个直接量。

## 直接量的类型

并不是所有的数据类型都可以指定直接量，能指定直接量的通常只有三种类型：基本类型、字符串类型和 null 类型。具体Java 支持如下 8 种类型的直接量。

### int 类型的直接量

在程序中直接给出的整型数值，可分为二进制、十进制、八进制和十六进制 4 种，其中二进制需要以 `0B` 或 `0b` 开头，八进制需要以 `0` 开头，十六进制需要以 `0x` 或 `0X` 开头。

**例**：`123`、`012`(对应十进制的 10)、`0x12`(对应十进制的 18)

### long 类型的直接量

在整型数值后添加 `l` 或 `L` 后就变成了 long 类型的直接量。

**例**：`3L`、`0x12L`(对应十进制的 18L)

### float 类型的直接量

在一个浮点数后添加 `f` 或 `F` 就变成了 float 类型的直接量，这个浮点数可以是标准小数形式，也可以是科学计数法形式。

**例**：`5.34F`、`3.14E5f`

### double 类型的直接量

直接给出一个标准小数形式或者科学计数法形式的浮点数就是 double 类型的直接量。

**例**：5.34、3.14E5。

### boolean 类型的直接量

这个类型的直接量只有 `true` 和 `false`。

### char 类型的直接量

char 类型的直接量有三种形式，分别是用单引号括起来的字符、转义字符和 Unicode 值表示的字符。

**例**：`'a'`，`'\n'`和`'\u0061'`

### String 类型的直接量

一个用双引号括起来的字符序列就是 String 类型的直接量。

在大多数其他语言中，包括 C/C++，字符串作为字符的数组被实现。然而，在 Java 中并非如此。在 Java 中，字符串实际上是对象类型。因为 Java 对字符串是作为对象实现的，因此，它有广泛的字符串处理能力，而且功能既强又好用。

### null 类型的直接量

这个类型的直接量只有一个值，即 `null`。

在上面的 8 种类型的直接量中，null 类型是一种特殊类型，它只有一个值：`null`。而且这个直接量可以赋给任何引用类型的变量，用以表示这个引用类型变量中保存的地址为空，即还未指向任何有效对象。

## 直接量的赋值

通常总是把一个直接量赋值给对应类型的变量：

```java
int a = 5;
char c = 'a';
boolean b = true;
float f = 5.12f;
double d = 4.12;
String name = "nihao";
String url = "http://www.baidu.com";
```

除此之外，Java 还支持数值之间的自动类型转换，因此允许把一个数值直接量直接赋给另一种类型的变量，这种赋值必须是系统所支持的自动类型转换，例如把 int 类型的直接量赋给一个 long 类型的变量。

String 类型的直接量不能赋给其他类型的变量，null 类型的直接量可以直接赋给任何引用类型的变量，包括 String 类型。boolean 类型的直接量只能赋给 boolean 类型的变量，不能赋给其他任何类型的变量。

关于字符串直接量有一点需要指出，当程序第一次使用某个字符串直接量时，Java 会使用常量池(`constant pool`)来缓存该字符串直接量，如果程序后面的部分需要用到该字符串直接量时，Java 会直接使用常量池(`constant pool`)中的字符串直接量。

提示：

- 由于 String 类是一个典型的不可变类，因此 String 对象创建出来的就不可能改变，因此无需担心共享 String 对象会导致混乱。
- 常量池(`constant pool`)指的是在编译期被确定，并被保存在已编译的 .class 文件中的一些数据，它包括关于类、方法、接口中的常量，也包括字符串直接量。

```java
String s0 = "hello";
String s1 = "hello";
String s2 = "he" + "llo";
System.out.println(s0 == s1);System.out.println(s0 == s2);
```

运行结果为：

> true
> true

Java 会确保每个字符串常量只有一个，不会产生多个副本。例子中的 s0 和 s1 中的“hello”都是字符串常量，它们在编译期就被确定了，所以 `s0 = s1` 返回 true。而“he”和“llo”也都是字符串常量，当一个字符串由多个字符串常量连接而成时，它本身也是字符串常量，s2 同样在编译期就被解析为一个字符串常量，所以 s2 也是常量池中“hello”的引用。因此，程序输出 `s0 == s1` 返回 true，`s1 == s2` 也返回 true。