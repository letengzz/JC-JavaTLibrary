# Scanner从键盘获取

从键盘获取不同类型的变量 使用`Scanner` 类

**步骤**：

 1. 首先通过`import`语句导入`java.util.Scanner`包： 

    ```java
    import java.util.Scanner;
    ```

 2. 创建`Scanner`对象并传入`System.in`。`System.out`代表标准输出流，而`System.in`代表标准输入流。直接使用`System.in`读取用户输入虽然是可以的，但需要更复杂的代码，而通过`Scanner`就可以简化后续的代码。

    ```java
    Scanner scanner = new Scanner(System.in);
    ```

 3. [调用scanner类的相关方法](../../Advanced/Object_Oriented/Class/Commonly_Class/Scanner.md)，来获取指定类型的变量：

    ![6](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207271440769.png)

**注意**：

- 需要根据相应的方法，来输入制定类型的值，如果输入的数据类型与要求的不匹配，报异常，导致程序终止。

- 对于char 的获取 Scanner 没有提供相关的方法，只能获取一个字符串：

  ```java
  String gender = scan.next();
  char genderChar = gender.charAt(0) //获取索引值为0位置上的字符
  ```

```java
import java.util.Scanner;

public class Scanner获取 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入一个整数:");
        int i = scanner.nextInt();//获取整型
        System.out.println(i);
        
		System.out.println("请输入一个字符串:");
        String name = scanner.next();//获取字符串
        System.out.println(name);
    }
}
```

# print向屏幕输出

向屏幕输出一些内容，使用`System.out.println()`

`println`是print line的缩写，表示输出并换行。如果输出后不想换行，可以用`print()`

- `System.out.println();`：先输出数据,然后换行。

- `System.out.print();`：只输出数据。

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("A,");
        System.out.print("B,");
        System.out.print("C.");
        System.out.println();
        System.out.println("END");
    }
}
```

**格式化输出**：

​	如果要把数据显示成期望的格式，就需要使用格式化输出的功能。格式化输出使用`System.out.printf()`，通过使用占位符`%?`，`printf()`可以把后面的参数格式化成指定格式：

```java
public class Main {
    public static void main(String[] args) {
        double d = 3.1415926;
        System.out.printf("%.2f\n", d); // 显示两位小数3.14
        System.out.printf("%.4f\n", d); // 显示4位小数3.1416
    }
}
```

Java的格式化功能提供了多种占位符，可以把各种数据类型“格式化”成指定的字符串：

| 占位符 |               说明               |
| :----: | :------------------------------: |
|  `%d`  |          格式化输出整数          |
|  `%x`  |      格式化输出十六进制整数      |
|  `%f`  |         格式化输出浮点数         |
|  `%e`  | 格式化输出科学计数法表示的浮点数 |
|  `%s`  |           格式化字符串           |

注意，由于`%`表示占位符，因此，连续两个`%%`表示一个`%`字符本身。

占位符本身还可以有更详细的格式化参数。下面的例子把一个整数格式化成十六进制，并用0补足8位：

```java
public class Main {
    public static void main(String[] args) {
        int n = 12345000;
        System.out.printf("n=%d, hex=%08x", n, n); // 注意，两个%占位符必须传入两个数
    }
}
```

详细的格式化参数请参考JDK文档[java.util.Formatter](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Formatter.html#syntax)
