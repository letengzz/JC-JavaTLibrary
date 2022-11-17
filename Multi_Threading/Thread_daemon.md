# 守护线程

守护线程是指在程序运行时在后台提供 一种通用服务的线程，守护线程又称为"服务进程"、"后台线程"，如果其他的线程都执行完毕，也就是没有了被守护这，守护线程也就没有工作可以做了，也就没有继续运行的必要了，进程会停掉所有守护线程，退出程序。

JVM的垃圾回收线程就是典型的守护线程。

设置为守护线程，只需要在调用`start()`方法启动之前调用线程的`setDaemon(true)`方法即可，若在start()之后调用，则会抛出java.lang.IllegalThreadStateException异常，该线程仍默认为用户线程(应用程序里的自定义线程)。

**注意**：

- 在守护线程内创建的线程也是守护线程。
- 循环没有终止的条件，但是当主线程结束时，守护线程没有了被守护着，也会结束。
- 守护线程不应该访问、写入持久化资源，如文件、数据库，因为它随时可能会被停止，这样就容易导致资源未释放，数据写入中断等问题。

```java
public class ThreadDaemon {
    public static void main(String[] args) {
        Thread t1 = new Thread(()->{
            Thread  t2 = new Thread(()->System.out.println("在守护线程内创建的线程是"+isDaemonThread()));
            t2.start();

            //当用户线程执行完成后，守护线程也会停止执行
            int i = 1;
            while (true){
                try {
                    TimeUnit.MICROSECONDS.sleep(500);
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
                System.out.println("t:"+isDaemonThread()+",count="+i++);
            }
        });
        //设置t线程为守护线程
        t1.setDaemon(true);
        t1.start();
        //主线程
        System.out.println("主线程["+isDaemonThread()+"]执行开始");
        try {
            TimeUnit.MICROSECONDS.sleep(2);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
        System.out.println("主线程["+isDaemonThread()+"]结束");
    }
    private static String isDaemonThread(){
        return Thread.currentThread().isDaemon()?"守护线程":"非守护线程";
    }
}
```











