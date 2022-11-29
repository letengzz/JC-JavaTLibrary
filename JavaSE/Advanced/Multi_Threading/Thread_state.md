# 线程的状态

在Java程序中，一个线程对象只能调用一次`start()`方法启动新线程，并在新线程中执行`run()`方法。一旦`run()`方法执行完毕，线程就结束了。

**Java线程的状态**：

- **新建状态**(New)：新创建的线程，尚未执行
- **就绪状态**(Runnable)：运行中的线程，正在执行`run()`方法的Java代码
- **运行状态**(Running)：就绪状态的线程获取到了CPU的执行权，正在运行
- **阻塞状态**(Blocked)：运行中的线程，因为某些操作被阻塞而挂起
  - **等待阻塞**(Waiting)：运行中的线程，因为某些操作在等待中
  - **同步阻塞**：运行的线程获取对象的同步**锁**时，同步锁被别的线程暂用，JVM就会把该线程放入锁池中
  - **其他阻塞**：运行的线程遇到了`sleep()`(Timed Waiting：运行中的线程，因为执行`sleep()`方法正在计时等待)或者join方法，或者发出了I/O请求，JVM会把该线程置为阻塞状态

- **终止状态**(Terminated)：线程已终止，因为`run()`方法执行完毕

**状态转移图**：

![](https://cdn.jsdelivr.net/gh/letengzz/Two-C@mian/img/Java/202211061702782.gif)

当线程启动后，它可以在`Runnable`、`Blocked`、`Waiting`和`Timed Waiting`这几个状态之间切换，直到最后变成`Terminated`状态，线程终止。

**线程终止的原因**：

- 线程正常终止：`run()`方法执行到`return`语句返回
- 线程意外终止：`run()`方法因为未捕获的异常导致线程终止
- 对某个线程的`Thread`实例调用`stop()`方法强制终止（强烈不推荐使用）

## 查看运行状态

```java
Thread t = new Thread();
System.out.println(t.getState());
```
