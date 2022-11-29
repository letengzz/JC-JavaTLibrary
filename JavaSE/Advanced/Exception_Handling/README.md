# 异常处理

在程序设计和运行的过程中，对于错误的处理是极其重要的，任何程序都很难做到百分百完美。尽管 Java 语言的设计从根本上提供了便于写出整洁、安全代码的方法，并且程序员也尽量地减少错误的产生，但是使程序被迫停止的错误的存在仍然不可避免。为此，Java 提供了异常处理机制来帮助程序员检查可能出现的错误，以保证程序的可读性和可维护性。**Java 的异常处理机制可以让程序具有极好的容错性，让程序更加健壮**。

Java 的异常处理通过 5 个关键字来实现：`try`、`catch`、`throw`、`throws` 和 `finally`。`try` `catch` 语句用于捕获并处理异常，`finally` 语句用于在任何情况下(除特殊情况外)都必须执行的代码，`throw` 语句用于拋出异常，`throws` 语句用于声明可能会出现的异常。

- [Java异常处理概述](exception_handling.md)
- [异常类型](exception_types.md)
- [捕获异常](exception_catch.md)
- [声明和抛出异常](exception_throws_declare.md)
- [自定义异常](exception_custom.md)
- [多异常捕获](exception_multiple .md)
- [总结](conclusion.md)
- [练习](../../)

**扩展**：

- [空指针异常`NullPointerException`](NullPointerException.md)
- [使用断言](Assertion.md)
- [Java中Error和Exception的异同](error_exception.md)
- [Java 9增强的自动资源管理](automatic_resource_management.md)
- [Java的异常跟踪栈](stack_trace.md)

**日志**：

- [Java.util.logging记录日志](Log/JDKLogging/README.md)
- [使用Commons Logging和Log4j记录日志](Log/logging_log4j.md)
- [使用SLF4J和Logback记录日志](Log/slf4j_logback.md)