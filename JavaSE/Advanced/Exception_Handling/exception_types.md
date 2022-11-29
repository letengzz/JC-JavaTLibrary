# 异常类型

为了能够及时有效地处理程序中的运行错误，Java 专门引入了异常类。在 Java 中所有异常类型都是内置类 `java.lang.Throwable` 类的子类，即 Throwable 位于异常类层次结构的顶层。Throwable 类下有两个异常分支 `Exception`和`Error`

从继承关系可知：`Throwable`是异常体系的根，它继承自`Object`。`Throwable`有两个体系：`Error`和`Exception`

**Java规定**：

- 必须捕获的异常，包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为`Checked Exception`。
- 不需要捕获的异常，包括`Error`及其子类，`RuntimeException`及其子类。

因为Java的异常是`class`，它的**继承关系**：

![image-20220808124424591](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208081244520.png)

## Throwable

`Throwable` 类是所有异常和错误的超类(根)，继承自Object。

Throwable分为：

- `Exception`类用于用户程序可能出现的异常情况，它也是用来创建自定义异常类型类的类。
- `Error`定义了在通常环境下不希望被程序捕获的异常。一般指的是 JVM 错误，如堆栈溢出。

### Error 错误

`Error`表示Java无法解决的严重问题，通常是灾难性的致命错误，不是程序可以控制的，程序对此一般无能为力。**一般不编写针对性代码进行处理**。

**例**：

- `OutOfMemoryError`：内存耗尽
- `NoClassDefFoundError`：无法加载某个Class
- `StackOverflowError`：栈溢出

### Exception 异常

`Exception`是运行时的错误，它可以被捕获并处理。

某些异常是应用程序逻辑处理的一部分，应该捕获并处理：

- `NumberFormatException`：数值类型的格式错误
- `FileNotFoundException`：未找到文件
- `SocketException`：读取网络失败

还有一些异常是程序逻辑编写不对造成的，应该修复程序本身：

- `NullPointerException`：对某个`null`的对象调用方法或字段
- `IndexOutOfBoundsException`：数组索引越界

`Exception`分为两大类：

1. `RuntimeException`以及它的子类(**运行时异常**)。
2. 非`RuntimeException`，包括`IOException`、`ReflectiveOperationException`等等(**非运行时异常**)。

这两种异常有很大的区别，也称为**不检查异常**(`Unchecked Exception`)和**检查异常**(`Checked Exception`)。

**注意**：

- 编译器对`RuntimeException`及其子类不做强制捕获要求，不是指应用程序本身不应该捕获并处理`RuntimeException`。是否需要捕获，具体问题具体分析。

- 异常是一种`class`，因此它本身带有类型信息。异常可以在任何地方抛出，但只需要在上层捕获，这样就和方法调用分离了：

  ```java
  try {
      String s = processFile(“C:\\test.txt”);
      // ok:
  } catch (FileNotFoundException e) {
      // file not found:
  } catch (SecurityException e) {
      // no read permission:
  } catch (IOException e) {
      // io error:
  } catch (Exception e) {
      // other error:
  }
  ```

#### 运行时异常

运行时异常都是 `RuntimeException` 类及其子类异常，如 `NullPointerException`、`IndexOutOfBoundsException` 等，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。这些异常一般由程序逻辑错误引起，程序应该从逻辑角度尽可能避免这类异常的发生。

常见运行时异常：

![图片1](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208081625315.png)

#### 非运行时异常

非运行时异常是指 `RuntimeException` 以外的异常，类型上都属于 Exception 类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如 `IOException`、`ClassNotFoundException` 等以及用户自定义的 Exception 异常(一般情况下不自定义检查异常)。

常见非运行时异常：

![图片2](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208081625951.png)