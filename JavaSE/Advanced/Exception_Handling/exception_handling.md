# Java异常处理

**异常**(`exception`)是在编译运行程序时产生的一种异常情况。

Java中的异常又称为例外，是一个**在程序执行期间发生的事件，它中断正在执行程序的正常指令流**。为了能够及时有效地处理程序中的运行错误，必须使用**异常类**，这可以让程序具有极好的容错性且更加健壮。 

一个健壮的程序必须处理各种各样的错误(程序调用某个函数的时候，如果失败了，就表示出错)。

在 Java 中一个异常的产生，主要有如下三种**原因**：

1. Java 内部错误发生异常，Java 虚拟机产生的异常。
2. 编写的程序代码中的错误所产生的异常，例如空指针异常、数组越界异常等。
3. 通过`throw`语句手动生成的异常，一般用来告知该方法的调用者一些必要信息。

Java 通过面向对象的方法来处理异常。在一个方法的运行过程中，如果发生了异常，则这个方法会产生代表该异常的一个对象，并把它交给运行时的系统，运行时系统寻找相应的代码来处理这一异常。

[拋出(`throw`)异常](exception_throws_declare.md#throw 拋出异常)：生成异常对象，并把它提交给运行时系统的过程。

[捕获(`catch`)异常](exception_catch.md)：运行时系统在方法的调用栈中查找，直到找到能够处理该类型异常的对象的过程。

**获知调用失败的信息的两种方法**：

- 方法一：约定返回错误码。

  例如，处理一个文件，如果返回`0`，表示成功，返回其他整数，表示约定的错误码：

  ```java
  int code = processFile("C:\\test.txt");
  if (code == 0) {
      // ok:
  } else {
      // error:
      switch (code) {
      case 1:
          // file not found:
      case 2:
          // no read permission:
      default:
          // unknown error:
      }
  }
  ```

​		因为使用`int`类型的错误码，想要处理就非常麻烦。这种方式常见于底层C函数。

- 方法二：在语言层面上提供一个异常处理机制。

  Java内置了一套异常处理机制，总是使用异常来表示错误。

  ```java
  import java.io.UnsupportedEncodingException;
  import java.util.Arrays;
  
  public class Main {
      public static void main(String[] args) {
          byte[] bs = toGBK("中文");
          System.out.println(Arrays.toString(bs));
      }
  
      static byte[] toGBK(String s) {
          try {
              // 用指定编码转换String为byte[]:
              return s.getBytes("GBK");
          } catch (UnsupportedEncodingException e) {
              // 如果系统不支持GBK编码，会捕获到UnsupportedEncodingException:
              System.out.println(e); // 打印异常信息
              return s.getBytes(); // 尝试使用用默认编码
          }
      }
  }
  ```

# 异常处理机制

为了保证程序有效地执行，需要对发生的异常进行相应的处理。

Java 的异常处理通过 5 个关键字来实现：`try`、`catch`、`throw`、`throws` 和 `finally`。`try` `catch` 语句用于捕获并处理异常，`finally` 语句用于在任何情况下(除特殊情况外)都必须执行的代码，`throw`语句用于拋出异常，`throws` 语句用于声明可能会出现的异常。

Java的异常处理机制提供了一种结构性和控制性的方式来处理程序执行期间发生的事件。异常处理的机制如下：

- 在方法中用 `try` `catch` 语句捕获并处理异常，`catch` 语句可以有多个，用来匹配多个异常。
- 对于处理不了的异常或者要转型的异常，在方法的声明处通过 `throws` 语句拋出异常，即由上层的调用方法来处理。

# 异常处理基本结构

异常处理程序的**基本结构**：

```java
try {    
    逻辑程序块
} catch(ExceptionType1 e) {    
    处理代码块1
} catch (ExceptionType2 e) {    
    处理代码块2
    throw(e);    // 再抛出这个"异常"
} finally {    
    释放资源代码块
}
```

