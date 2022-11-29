# 加入线程(插入)

让一个线程等待另一个线程完成才继续执行，如A线程线程执行体中调用B线程的`join()`方法，则A线程被堵塞，直到B线程执行完为止，A才能得以继续执行。

`join()`没有时间参数，那么就得等加入的线程执行完毕才能执行，如果有时间参数，那么就相当于等待指令时间之后，继续执行

- 通过对另一个线程对象调用`join()`方法可以等待其执行结束

- 对已经运行结束的线程调用`join()`方法会立刻返回

**作用**：先将当前执行线程挂起，待其他线程结束后继续执行当前线程的代码。

**注意**：挂起的是当前正在执行的线程，不是挂起join方法的线程。

join方法有多种重载方法：

- `join()`：当前线程暂停，等待指定的线程执行结束后，当前线程再继续。
- `join(long millis)`：可以等待指定的毫秒数之后继续。
- `join(long millis,int nanos)`：等待该线程终止的时间最长为millis毫秒+nanos纳秒。

**例**：`main`线程在启动`t`线程后，可以通过`t.join()`等待`t`线程结束后再继续运行：

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            System.out.println("hello");
        });
        System.out.println("start");
        t.start();
        t.join();
        System.out.println("end");
    }
}
```

当`main`线程对线程对象`t`调用`join()`方法时，主线程将等待变量`t`表示的线程运行结束，即`join`就是指等待该线程结束，然后才继续往下执行自身线程。所以，上述代码打印顺序可以肯定是`main`线程先打印`start`，`t`线程再打印`hello`，`main`线程最后再打印`end`。

如果`t`线程已经结束，对实例`t`调用`join()`会立刻返回。此外，`join(long)`的重载方法也可以指定一个等待时间，超过等待时间后就不再继续等待。