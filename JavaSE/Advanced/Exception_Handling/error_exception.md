# Error和Exception的异同

[Error(错误)](exception_types.md#Error 错误)和 [Exception(异常)](exception_types.md#Exception 异常)都是 `java.lang.Throwable` 类的子类，在 Java 代码中只有继承了 [Throwable 类](exception_types.md#Throwable)的实例才能被[throw](exception_throws_declare.md#throw 拋出异常)或者[catch](exception_catch.md)。

Exception 和 Error 体现了 Java 平台设计者对不同异常情况的**分类**：

------

Exception 是程序正常运行过程中可以预料到的意外情况，并且应该被开发者捕获，进行相应的处理。

Exception 又分为可检查(`checked`)异常和不检查(`unchecked`)异常，可检查异常在源码里必须显示的进行捕获处理，这里是编译期检查的一部分。不检查异常就是所谓的运行时异常，通常是可以编码避免的逻辑错误，具体根据需要来判断是否需要捕获，并不会在编译器强制要求。

------

Error 是指正常情况下不大可能出现的情况，绝大部分的 Error 都会导致程序处于非正常、不可恢复状态。所以不需要被开发者捕获。

Error 错误是任何处理技术都无法恢复的情况，肯定会导致程序非正常终止。并且 Error 错误属于未检查类型，大多数发生在运行时。

------

常见的 Error 和 Exception：

- 运行时异常(`RuntimeException`)：

  - **空指针异常**：`NullPropagation`

  - **类型强制转换异常**：`ClassCastException`

  - **传递非法参数异常**：`IllegalArgumentException`
  - **下标越界异常**：`IndexOutOfBoundsException`
  - **数字格式异常**：`NumberFormatException`

- 非运行时异常(非`RuntimeException`)：

  - **找不到指定 class 的异常**：`ClassNotFoundException`
  - **IO 操作异常**：`IOException`

- 错误(`Error`)：

  - **找不到 class 定义异常**：`NoClassDefFoundError`

  - **深递归导致栈被耗尽而抛出的异常**：`StackOverflowError`

  - **内存溢出异常**：`OutOfMemoryError`

下面代码会导致 Java 堆栈溢出错误：

```java
// 通过无限递归演示堆栈溢出错误
class StackOverflow {    
    public static void test(int i) {        
        if (i == 0) {            
            return;        
        } else {            
            test(i++);        
        }    
    }
}
public class ErrorEg {    
    public static void main(String[] args) {        
        // 执行StackOverflow方法        
        StackOverflow.test(5);    
    }
}
```

运行输出为：

> Exception in thread "main" java.lang.StackOverflowError
>   at ch11.StackOverflow.test(ErrorEg.java:9)
>   at ch11.StackOverflow.test(ErrorEg.java:9)
>   at ch11.StackOverflow.test(ErrorEg.java:9)
>   at ch11.StackOverflow.test(ErrorEg.java:9)

上面代码通过无限递归调用最终引发了 `java.lang.StackOverflowError` 错误。