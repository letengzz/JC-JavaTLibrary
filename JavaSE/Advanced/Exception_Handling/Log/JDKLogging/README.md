# JDK自带记录日志类`Java.util.logging`

在有问题的代码中使用 `System.out.println` 方法在控制台打印消息，来帮助观察程序运行的操作过程。如果使用  `System.out.println` 方法，一旦发现问题的根源，就要将这些语句从代码中删去。如果接下来又出现了问题，就需要再插入几个调用 `System.out.println` 方法的语句，如此反复，增加了工作量。

**日志**用来记录程序的运行轨迹，方便查找关键信息，也方便快速定位解决问题。

输出日志，而不是用`System.out.println()`，有以下几个好处：

1. 可以设置输出样式，避免自己每次都写`"ERROR: " + var`；
2. 可以设置输出级别，禁止某些级别输出。例如，只输出错误日志；
3. 可以被重定向到文件，这样可以在程序运行结束后查看日志；
4. 可以按包名控制日志级别，只输出某些包打的日志；
5. 可以……

Java标准库内置了日志包`java.util.logging`，可以直接使用：

```java
import java.util.logging.Level;
import java.util.logging.Logger;
public class Hello {
    public static void main(String[] args) {
        Logger logger = Logger.getGlobal();
        logger.info("start process...");
        logger.warning("memory is running out...");
        logger.fine("ignored.");
        logger.severe("process will be terminated...");
    }
}
```

运行，输出结果：

> Mar 02, 2019 6:32:13 PM Hello main
> INFO: start process...
> Mar 02, 2019 6:32:13 PM Hello main
> WARNING: memory is running out...
> Mar 02, 2019 6:32:13 PM Hello main
> SEVERE: process will be terminated...

使用日志的**优点**：自动打印了时间、调用类、调用方法等很多有用的信息。

如果要生成简单的日志记录，可以使用全局日志记录器并调用其 `info` 方法：

```java
Logger.getGlobal().info("打印信息");
```

JDK Logging 把日志分为如下表 7 个级别，等级依次降低：

![图片3](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208102130209.png)


Logger 的**默认级别**是 `INFO`，比 `INFO` 级别低的日志将不显示。用日志级别的好处在于，调整级别，就可以屏蔽掉很多调试相关的日志输出。Logger 的默认级别定义在 jre 安装目录的 lib 下面。

```shell
# Limit the message that are printed on the console to INFO and above.
java.util.logging.ConsoleHandler.level = INFO
```

所以在默认情况下，日志只显示前三个级别，对于所有的级别有下面几种记录方法：

```java
logger.warning(message);
logger.fine(message);
```

同时，还可以使用 log 方法指定级别：

```java
logger.log(Level.FINE, message);
```

**例**：

```java
public class Test {
    private static Logger log = Logger.getLogger(Test.class.toString());

    public static void main(String[] args) {
        // 级别依次升高，后面的日志级别会屏蔽之前的级别
        log.finest("finest");
        log.finer("finer");
        log.fine("fine");
        log.config("config");
        log.info("info");
        log.warning("warning");
        log.severe("server");
    }
}
```

输出结果为：

> 十一月 27, 2019 5:13:05 下午 Test.Test main
> 信息: info
> 十一月 27, 2019 5:13:05 下午 Test.Test main
> 警告: warning
> 十一月 27, 2019 5:13:05 下午 Test.Test main
> 严重: server

**可以使用 `setLevel` 方法设置级别**

**例**：`logger.setLevel(Level.FINE);`可以将 `FINE` 和更高级别的都记录下来。还可以使用 `Level.ALL` 开启所有级别的记录，或者使用 `Level.OFF` 关闭所有级别的记录。

**注意**：如果将记录级别设计为 `INFO` 或者更低，则需要修改日志处理器的配置。默认的日志处理器不会处理低于 `INFO` 级别的信息。

使用Java标准库内置的Logging有以下**局限**：

- Logging系统在JVM启动时读取配置文件并完成初始化，一旦开始运行`main()`方法，就无法修改配置；

- 配置不太方便，需要在JVM启动时传递参数`-Djava.util.logging.config.file=<config-file-name>`。

因此，Java标准库内置的Logging使用并不是非常广泛。

# 修改日志管理器配置

可以通过编辑配置文件来修改日志系统的各种属性。在默认情况下，配置文件存在于 jre 安装目录下"`jre/lib/logging.properties`"。要想使用另一个配置文件，就要将 `java.util.logging.config.file` 特性设置为配置文件的存储位置，并用下列命令启动应用程序。

```java
java -Djava.util.logging.config.file = configFile MainClass
```

日志管理器在 JVM 启动过程中初始化，这在 main 执行之前完成。如果在 main 中调用`System.setProperty("java.util.logging.config.file",file)`，也会调用`LogManager.readConfiguration()`来重新初始化日志管理器。

要想修改默认的日志记录级别，就需要编辑配置文件，并修改以下命令行。

`.level=INFO`

可以通过添加以下内容来指定自己的日志记录级别

`Test.Test.level=FINE`

也就是说，在日志记录器名后面添加后缀 `.level`。

在稍后可以看到，日志记录并不将消息发送到控制台上，这是处理器的任务。另外，处理器也有级别。要想在控制台上看到 `FINE` 级别的消息，就需要进行下列设置。

```java
java.util.logging.ConsoleHandler.level=FINE
```

**注意**：在日志管理器配置的属性设置不是系统属性，因此，用`-Dcom.mycompany.myapp.level=FINE`启动应用程序不会对日志记录器产生任何影响。

**总结**：

- 日志是为了替代`System.out.println()`，可以定义格式，重定向到文件等；
- 日志可以存档，便于追踪问题；
- 日志记录可以按级别分类，便于打开或关闭某些级别；
- 可以根据配置文件调整日志，无需修改代码；
- Java标准库提供了`java.util.logging`来实现日志功能。