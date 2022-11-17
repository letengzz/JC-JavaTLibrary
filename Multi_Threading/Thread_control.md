# 线程控制

## 获取名称和设置名称

获取当前线程：

```java
static Thread currentThread()  
```

**例**：

```java
public class Demo {
    public static void main(String[] args) {
        Thread main = Thread.currentThread();
        System.out.println(main);
    }
}
```

获取通过 `getName()`方法获取线程对象的名字：

```java
package 取值赋值04;

public class Demo {
    public static void main(String[] args) {
        Thread main = Thread.currentThread();
        //获取main线程名称
        System.out.println(main.getName());
    }
}

```

给线程名字赋值：

```java
package 取值赋值04;

public class Demo {
    public static void main(String[] args) {
        Thread main = Thread.currentThread();
        //获取main线程名称
        System.out.println(main.getName());
        //赋值
        main.setName("明天要学习");
        System.out.println(main.getName());

    }
}

```

## 线程休眠

当强迫当前线程暂停一段时间时，可以调用`Thread.sleep()`实现，指定等待时间，超过等待时间线程仍然没有结束就不再等待。

`sleep()`传入的参数是毫秒。调整暂停时间的大小。

```java
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread() {
            public void run() {
                System.out.println("thread run...");
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {}
                System.out.println("thread end.");
            }
        };
        t.start();
}
```
