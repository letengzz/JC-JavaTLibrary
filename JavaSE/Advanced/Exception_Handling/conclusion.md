## 总结

- Java使用异常来表示错误，并通过`try ... catch`捕获异常；

- Java的异常是`class`，并且从`Throwable`继承；

- `Error`是无需捕获的严重错误，`Exception`是应该捕获的可处理的错误；

- `RuntimeException`无需强制捕获，非`RuntimeException`（Checked Exception）需强制捕获，或者用`throws`声明；

- 不推荐捕获了异常但不进行任何处理，可以调用`printStackTrace()`方法打印异常栈。