# Java的异常跟踪栈

异常对象的 `printStackTrace()` 方法用于打印异常的跟踪栈信息，根据 `printStackTrace()` 方法的输出结果，开发者可以找到异常的源头，并跟踪到异常一路触发的过程。

用于测试 `printStackTrace` 的例子程序：

```java
class SelfException extends RuntimeException {
    SelfException() {
    }

    SelfException(String msg) {
        super(msg);
    }
}

public class PrintStackTraceTest {
    public static void main(String[] args) {
        firstMethod();
    }

    public static void firstMethod() {
        secondMethod();
    }

    public static void secondMethod() {
        thirdMethod();
    }

    public static void thirdMethod() {
        throw new SelfException("自定义异常信息");
    }
}
```

上面程序中 main 方法调用 `firstMethod`，`firstMethod` 调用 `secondMethod`，`secondMethod` 调用 `thirdMethod`，`thirdMethod` 直接抛出一个 `SelfException` 异常。运行上面程序，会看到如下所示的结果。

> Exception in thread "main" Test.SelfException: 自定义异常信息
>     at Test.PrintStackTraceTest.thirdMethod(PrintStackTraceTest.java:26)
>     at Test.PrintStackTraceTest.secondMethod(PrintStackTraceTest.java:22)
>     at Test.PrintStackTraceTest.firstMethod(PrintStackTraceTest.java:18)
>     at Test.PrintStackTraceTest.main(PrintStackTraceTest.java:14)

上面运行结果的第 2 行到第 5 行之间的内容是异常跟踪栈信息，从打印的异常信息我们可以看出，异常从 `thirdMethod` 方法开始触发，传到 `secondMethod` 方法，再传到 `firstMethod` 方法，最后传到 main 方法，在 main 方法终止，这个过程就是 Java 的**异常跟踪栈**。

在面向对象的编程中，大多数复杂操作都会被分解成一系列方法调用。这是因为实现更好的可重用性，将每个可重用的代码单元定义成方法，将复杂任务逐渐分解为更易管理的小型子任务。由于一个大的业务功能需要由多个对象来共同实现，**在最终编程模型中，很多对象将通过一系列方法调用来实现通信，执行任务**。

面向对象的应用程序运行时，经常会发生一系列方法调用，从而形成"**方法调用栈**"，异常的传播则相反：**只要异常没有被完全捕获(包括异常没有被捕获，或异常被处理后重新抛出了新异常)，异常从发生异常的方法逐渐向外传播，首先传给该方法的调用者，该方法调用者再次传给其调用者……，直至最后传到 main 方法，如果 main 方法依然没有处理该异常，则 JVM 会中止该程序，并打印异常的跟踪栈信息。**

结果中的异常跟踪栈信息非常清晰，它记录了应用程序中执行停止的各个点。

异常跟踪栈信息的第一行一般详细显示异常的类型和异常的详细消息，接下来是所有异常的发生点，各行显示被调用方法中执行的停止位置，并标明类、类中的方法名、与故障点对应的文件的行。一行行地往下看，跟踪栈总是最内部的被调用方法逐渐上传，直到最外部业务操作的起点，通常就是程序的入口 main 方法或 `Thread` 类的 `run` 方法（多线程的情形）。

多线程程序中发生异常的情形：

```java
public class ThreadExceptionTest implements Runnable {
    public void run() {
        firstMethod();
    }

    public void firstMethod() {
        secondMethod();
    }

    public void secondMethod() {
        int a = 5;
        int b = 0;
        int c = a / b;
    }

    public static void main(String[] args) {
        new Thread(new ThreadExceptionTest()).start();
    }
}
```

运行上面程序，会看到如下运行结果：

> Exception in thread "Thread-0" java.lang.ArithmeticException: / by zero
>       at Test.ThreadExceptionTest.secondMethod(ThreadExceptionTest.java:14)
>       at Test.ThreadExceptionTest.firstMethod(ThreadExceptionTest.java:8)
>       at Test.ThreadExceptionTest.run(ThreadExceptionTest.java:4)
>       at java.lang.Thread.run(Unknown Source)

多线程异常的跟踪栈，从发生异常的方法开始，到线程的 run 方法结束。从上面的运行结果可以看出，程序在 `Thread` 的 `run` 方法中出现了 `ArithmeticException` 异常，这个异常的源头是 `ThreadExcetpionTest` 的 `secondMethod` 方法，位于 `ThreadExcetpionTest.java` 文件的 14 行。这个异常传播到 `Thread` 类的 `run` 方法就会结束（如果该异常没有得到处理，将会导致该线程中止运行）。

调用 `Exception` 的 `printStackTrace()` 方法就是打印该异常的跟踪栈信息，也就会看到上面两个示例运行结果中的信息。当然，如果方法调用的层次很深，将会看到更加复杂的异常跟踪栈。

**提示**：虽然 `printStackTrace()` 方法可以很方便地用于追踪异常的发生情况，可以用它来调试程序，但在最后发布的程序中，应该避免使用它。应该对捕获的异常进行适当的处理，而不是简单地将异常的跟踪栈信息打印出来。