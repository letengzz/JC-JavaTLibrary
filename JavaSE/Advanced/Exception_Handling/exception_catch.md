# 捕获异常

捕获异常使用`try...catch`语句，把可能发生异常的代码放到`try {...}`中，然后使用`catch`捕获对应的`Exception`及其子类：

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) {
        try {
            // 用指定编码转换String为byte[]:
            return s.getBytes("GBK");
        } catch (UnsupportedEncodingException e) {
            // 如果系统不支持GBK编码，会捕获到UnsupportedEncodingException:
            System.out.println(e); // 打印异常信息
            return s.getBytes(); // 尝试使用用默认编码
        }
    }
}
```

如果我们不捕获`UnsupportedEncodingException`，会出现编译失败的问题：

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) {
        return s.getBytes("GBK");
    }
}
```

编译器会报错，错误信息类似：`unreported exception UnsupportedEncodingException; must be caught or declared to be thrown`，并且准确地指出需要捕获的语句是`return s.getBytes("GBK");`。意思是说，像`UnsupportedEncodingException`这样的`Checked Exception`，必须被捕获。

这是因为`String.getBytes(String)`方法定义是：

```java
public byte[] getBytes(String charsetName) throws UnsupportedEncodingException {
    ...
}
```

在方法定义的时候，使用`throws Xxx`表示该方法可能抛出的异常类型。调用方在调用的时候，必须强制捕获这些异常，否则编译器会报错。

在`toGBK()`方法中，因为调用了`String.getBytes(String)`方法，就必须捕获`UnsupportedEncodingException`。我们也可以不捕获它，而是在方法定义处用throws表示`toGBK()`方法可能会抛出`UnsupportedEncodingException`，就可以让`toGBK()`方法通过编译器检查：

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        return s.getBytes("GBK");
    }
}
```

上述代码仍然会得到编译错误，但这一次，编译器提示的不是调用`return s.getBytes("GBK");`的问题，而是`byte[] bs = toGBK("中文");`。因为在`main()`方法中，调用`toGBK()`，没有捕获它声明的可能抛出的`UnsupportedEncodingException`。

修复方法是在`main()`方法中捕获异常并处理：

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        return s.getBytes("GBK");
    }
}
```

可见，只要是方法声明的Checked Exception，不在调用层捕获，也必须在更高的调用层捕获。所有未捕获的异常，最终也必须在`main()`方法中捕获，不会出现漏写`try`的情况。这是由编译器保证的。`main()`方法也是最后捕获`Exception`的机会。

如果是测试代码，上面的写法就略显麻烦。如果不想写任何`try`代码，可以直接把`main()`方法定义为`throws Exception`：

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws Exception {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        // 用指定编码转换String为byte[]:
        return s.getBytes("GBK");
    }
}
```

因为`main()`方法声明了可能抛出`Exception`，也就声明了可能抛出所有的`Exception`，因此在内部就无需捕获了。代价就是一旦发生异常，程序会立刻退出。

还可以在`toGBK()`内部“消化”异常：

```java
static byte[] toGBK(String s) {
    try {
        return s.getBytes("GBK");
    } catch (UnsupportedEncodingException e) {
        // 什么也不干
    }
    return null;
}
```

这种捕获后不处理的方式是非常不好的，即使真的什么也做不了，也要先把异常记录下来：

```java
static byte[] toGBK(String s) {
    try {
        return s.getBytes("GBK");
    } catch (UnsupportedEncodingException e) {
        // 先记下来再说:
        e.printStackTrace();
    }
    return null;
```

所有异常都可以调用`printStackTrace()`方法打印异常栈，这是一个简单有用的快速打印异常的方法。

**注意**：

- Java使用异常来表示错误，并通过`try ... catch`捕获异常

- Java的异常是`class`，并且从`Throwable`继承

- `Error`是无需捕获的严重错误，`Exception`是应该捕获的可处理的错误

- `RuntimeException`无需强制捕获，非`RuntimeException`(Checked Exception)需强制捕获，或者用`throws`声明

- 不推荐捕获了异常但不进行任何处理。

# try catch语句

在 Java 中通常采用 try-catch 语句来捕获异常并处理。

**语法格式**：

```java
try {    
    // 可能发生异常的语句
} catch(ExceptionType e) {    
    // 处理异常语句
}
```

在以上语法中，把可能引发异常的语句封装在 `try` 语句块中，用以捕获可能发生的异常。`catch` 后的`( )`里放匹配的异常类，指明 `catch` 语句可以处理的异常类型，发生异常时产生异常类的实例化对象。

如果 `try` 语句块中发生异常，那么一个相应的异常对象就会被拋出，然后 `catch` 语句就会依据所拋出异常对象的类型进行捕获，并处理。处理之后，程序会跳过 `try` 语句块中剩余的语句，转到 `catch` 语句块后面的第一条语句开始执行。

如果 `try` 语句块中没有异常发生，那么 `try` 块正常结束，后面的 `catch` 语句块被跳过，程序将从 `catch` 语句块后的第一条语句开始执行。

**注意**：`try...catch` 与 `if...else` 不一样，`try` 后面的花括号`{ }`不可以省略，即使 `try` 块里只有一行代码，也不可省略这个花括号。与之类似的是，`catch` 块后的花括号`{ }`也不可以省略。另外，`try` 块里声明的变量只是代码块内的局部变量，它只在 `try` 块内有效，其它地方不能访问该变量。

可以使用以下 3 个方法**输出相应的异常信息**：

- `printStackTrace()`方法：指出异常的类型、性质、栈层次及出现在程序中的位置（关于 printStackTrace 方法的使用可参考[Java的异常跟踪栈](stack_trace.md)）。
- `getMessage()`方法：输出错误的性质。
- `toString()`方法：给出异常的类型与性质。

**例**：

编写一个录入学生姓名、年龄和性别的程序，要求能捕捉年龄不为数字时的异常：

```java
import java.util.Scanner;
public class Test02 {    
    public static void main(String[] args) {        
        Scanner scanner = new Scanner(System.in);        
        System.out.println("---------学生信息录入---------------");        
        String name = ""; // 获取学生姓名        
        int age = 0; // 获取学生年龄        
        String sex = ""; // 获取学生性别        
        try {            
            System.out.println("请输入学生姓名：");            
            name = scanner.next();            
            System.out.println("请输入学生年龄：");            
            age = scanner.nextInt();            
            System.out.println("请输入学生性别：");            
            sex = scanner.next();        
        } catch (Exception e) {            
            e.printStackTrace();            
            System.out.println("输入有误！");        
        }        
        System.out.println("姓名：" + name);        
        System.out.println("年龄：" + age);    
    }
}
```

上述代码在 main() 方法中使用 `try catch` 语句来捕获异常，将可能发生异常的`age = scanner.nextlnt();`代码放在了 `try` 块中，在 `catch` 语句中指定捕获的异常类型为 Exception，并调用异常对象的 `printStackTrace()` 方法输出异常信息。运行结果：

> ---------学生信息录入---------------
> 请输入学生姓名：
> 徐白
> 请输入学生年龄：
> 110a
> java.util.InputMismatchException
>  at java.util.Scanner.throwFor(Unknown Source)
>  at java.util.Scanner.next(Unknown Source)
>  at java.util.Scanner.nextInt(Unknown Source)
>  at java.util.Scanner.nextInt(Unknown Source)
> 输入有误！
> 姓名：徐白
> 年龄：0
>  at text.text.main(text.java:19)

# try catch finally语句

在实际开发中，根据 try catch 语句的执行过程，try 语句块和 catch 语句块有可能不被完全执行，而有些处理代码则要求必须执行。

例如，程序在 try 块里打开了一些物理资源(如数据库连接、网络连接和磁盘文件等)，这些物理资源都必须显式回收。

> Java的垃圾回收机制不会回收任何物理资源，垃圾回收机制只回收堆内存中对象所占用的内存。

所以为了确保一定能回收 try 块中打开的物理资源，异常处理机制提供了 `finally` 代码块，并且 Java 7 之后提供了[自动资源管理(`Automatic Resource Management`)技术](automatic_resource_management.md)。

`finally` 语句可以与 `try` `catch` 语句块匹配使用，**语法格式**：

```java
try {    
    // 可能会发生异常的语句
} catch(ExceptionType e) {    
    // 处理异常语句
} finally {    
    // 清理代码块
}
```

对于以上格式，无论是否发生异常(除特殊情况外)，`finally` 语句块中的代码都会被执行。

`finally` 语句也可以和 `try` 语句匹配使用，**语法格式**：

```java
try {    
    // 逻辑代码块
} finally {    
    // 清理代码块
}
```

使用 `try-catch-finally` 语句时需**注意**：

1. 异常处理语法结构中只有 `try` 块是必需的，如果没有 `try` 块，则不能有后面的 `catch` 块和 `finally` 块
2. `catch` 块和 `finally` 块都是可选的，但 `catch` 块和 `finally` 块至少出现其中之一，也可以同时出现
3. 可以有多个 `catch` 块，捕获父类异常的 `catch` 块必须位于捕获子类异常的后面
4. 不能只有 `try` 块，既没有 `catch` 块，也没有 `finally` 块
5. 多个 `catch` 块必须位于 `try` 块之后，`finally` 块必须位于所有的 `catch` 块之后，最后执行。
6. `finally` 与 `try` 语句块匹配的语法格式，此种情况会导致异常丢失，所以不常见

一般情况下，无论是否有异常拋出，都会执行 finally 语句块中的语句。

**`try catch finally` 语句执行流程图**：

![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208092101878.jpeg)

`try catch finally` 语句块的执行情况可分为：

1. 如果 `try` 代码块中没有拋出异常，则执行完 `try` 代码块之后直接执行 finally 代码块，然后执行 `try catch finally` 语句块之后的语句。
2. 如果 `try` 代码块中拋出异常，并被 `catch` 子句捕捉，那么在拋出异常的地方终止 `try` 代码块的执行，转而执行相匹配的 `catch` 代码块，之后执行 `finally` 代码块。如果 `finally` 代码块中没有拋出异常，则继续执行 `try catch finally` 语句块之后的语句；如果 `finally` 代码块中拋出异常，则把该异常传递给该方法的调用者。
3. 如果 `try` 代码块中拋出的异常没有被任何 `catch` 子句捕捉到，那么将直接执行 `finally` 代码块中的语句，并把该异常传递给该方法的调用者。


除非在 `try` 块、`catch` 块中调用了退出虚拟机的方法`System.exit(int status)`，否则不管在 `try` 块或者 `catch` 块中执行怎样的代码，出现怎样的情况，异常处理的 `finally` 块总会执行。

通常情况下不在 `finally` 代码块中使用 `return` 或 `throw` 等导致方法终止的语句，否则将会导致 `try` 和 `catch` 代码块中的 `return` 和 `throw` 语句失效。

**例**： 当 Windows 系统启动之后，即使不作任何操作，在关机时都会显示“谢谢使用”：

```java
import java.util.Scanner;public class Test04 {    
    public static void main(String[] args) {        
        Scanner input = new Scanner(System.in);        
        System.out.println("Windows 系统已启动！");        
        String[] pros = { "记事本", "计算器", "浏览器" };        
        try {            
            // 循环输出pros数组中的元素            
            for (int i = 0; i < pros.length; i++) {                
                System.out.println(i + 1 + "：" + pros[i]);            
            }            
            System.out.println("是否运行程序：");            
            String answer = input.next();            
            if (answer.equals("y")) {                
                System.out.println("请输入程序编号：");                
                int no = input.nextInt();                
                System.out.println("正在运行程序[" + pros[no - 1] + "]");            
            }        
        } catch (Exception e) {            
            e.printStackTrace();        
        } finally {            
            System.out.println("谢谢使用!");        
        }    
    }
}
```

上述代码在 main() 方法中使用 `try catch finally` 语句模拟了系统的使用过程。当系统启动之后显示提示语，无论是否运行了程序，或者在运行程序时出现了意外，程序都将执行 finally 块中的语句，即显示“谢谢使用！”。输出时的结果如下所示。

> Windows 系统已启动！
> 1：记事本
> 2：计算器
> 3：浏览器
> 是否运行程序：
> y
> 请输入程序编号：
> 2
> 正在运行程序[计算器]
> 谢谢使用!
> Windows 系统已启动！
> 1：记事本
> 2：计算器
> 3：浏览器
> 是否运行程序：
> y
> 请输入程序编号：
> 5
> 谢谢使用!
> java.lang.ArrayIndexOutOfBoundsException: 4
>  at text.text.main(text.java:23)
>
> Windows 系统已启动！
> 1：记事本
> 2：计算器
> 3：浏览器
> 是否运行程序：
> asdfasd
> 谢谢使用!

# 多重catch语句

如果 `try` 代码块中有很多语句会发生异常，而且发生的异常种类又很多。那么可以在 `try` 后面跟有多个 `catch` 代码块。

多 `catch` 代码块**语法格式**：

```java
try {    
    // 可能会发生异常的语句
} catch(ExceptionType e) {    
    // 处理异常语句
} catch(ExceptionType e) {    
    // 处理异常语句
} catch(ExceptionType e) {    
    // 处理异常语句...
}
```

在多个 `catch` 代码块的情况下，当一个 `catch` 代码块捕获到一个异常时，其它的 `catch` 代码块就不再进行匹配。

**注意**：当捕获的多个异常类之间存在父子关系时，捕获异常时一般先捕获子类，再捕获父类。所以子类异常必须在父类异常的前面，否则子类捕获不到。

**例**：

```java
public class Test03 {    
    public static void main(String[] args) {        
        Date date = readDate();        
        System.out.println("读取的日期 = " + date);    
    }    
    public static Date readDate() {        
        FileInputStream readfile = null;        
        InputStreamReader ir = null;        
        BufferedReader in = null;        
        try {            
            readfile = new FileInputStream("readme.txt");            
            ir = new InputStreamReader(readfile);            
            in = new BufferedReader(ir);            // 读取文件中的一行数据            
            String str = in.readLine();            
            if (str == null) {                
                return null;            
            }            
            DateFormat df = new SimpleDateFormat("yyyy-MM-dd");            
            Date date = df.parse(str);            
            return date;        
        } catch (FileNotFoundException e) {            
            System.out.println("处理FileNotFoundException...");           
            e.printStackTrace();        
        } catch (IOException e) {            
            System.out.println("处理IOException...");            
            e.printStackTrace();        
        } catch (ParseException e) {            
            System.out.println("处理ParseException...");            
            e.printStackTrace();        
        }        
        return null;    
    }
}
```

上述代码通过 [Java I/O(输入输出)](../IO/README.md)流技术从文件 readme.txt 中读取字符串，然后解析成为日期。

在 `try` 代码块中调用 `FileInputStream` 构造方法可能会发生 `FileNotFoundException` 异常。调用 `BufferedReader` 输入流的 `readLine()` 方法可能会发生 `IOException` 异常。`FileNotFoundException` 异常是 `IOException` 异常的子类，应该先捕获 `FileNotFoundException` 异常；后捕获 `IOException` 异常。

如果将 `FileNotFoundException` 和 `IOException` 捕获顺序调换，那么捕获 `FileNotFoundException` 异常代码块将永远不会进入，`FileNotFoundException` 异常处理永远不会执行。  `ParseException` 异常与 `IOException` 和 `FileNotFoundException` 异常没有父子关系，所以捕获 `ParseException` 异常位置可以随意放置。