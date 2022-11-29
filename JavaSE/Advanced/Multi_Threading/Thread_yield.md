# 礼让线程

礼让线程，让当前正在执行的线程暂停，但不阻塞

使用`Thread.yield();`方法将线程从运行状态转为就绪状态。

**注意**：礼让不一定能成功，原理是让CPU重新调度

```java
public class testYield implements Runnable {

    @Override
    public void run() {
        //for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName() + "线程开始");
            System.out.println(Thread.currentThread().getName() + "线程结束");
        //}
    }
}

class yieldMain {
    public static void main(String[] args) {
        testYield testYield = new testYield();
        new Thread(testYield, "1").start();
        Thread.yield();
        new Thread(testYield, "2").start();
    }
}
```



