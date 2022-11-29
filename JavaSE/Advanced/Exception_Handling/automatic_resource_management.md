# Java 9增强的自动资源管理

当程序使用 `finally` 块关闭资源时，程序会显得异常臃肿：

```java
public static void main(String[] args) {    
    FileInputStream fis = null;    
    try {        
        fis = new FileInputStream("a.txt");    
    } catch (FileNotFoundException e) {        
        e.printStackTrace();    
    } finally {        
        // 关闭磁盘文件，回收资源        
        if (fis != null) {            
            try {                
                fis.close();            
            } catch (IOException e) {                
                e.printStackTrace();            
            }        
        }    
    }
}
```

Java 7 以前，上面程序中的 `finally` 代码块是不得不写的“臃肿代码”，为了解决这种问题，Java 7 增加了一个新特性，该特性提供了另外一种管理资源的方式，这种方式能自动关闭文件，被称为**自动资源管理**(`Automatic Resource Management`)。该特性是在 `try` 语句上的扩展，主要释放不再需要的文件或其他资源。

自动资源管理替代了 `finally` 代码块，并优化了代码结构和提高程序可读性。

**语法如下**：

```java 
try (声明或初始化资源语句) {    
    // 可能会生成异常语句
} catch(Throwable e1){    
    // 处理异常e1
} catch(Throwable e2){    
    // 处理异常e2
} catch(Throwable eN){    
    // 处理异常eN
}
```

当 `try` 代码块结束时，自动释放资源。不再需要显式的调用 `close()` 方法，该形式也称为"**带资源的 `try` 语句**"。

**注意**：

1. `try` 语句中声明的资源被隐式声明为 `final`，资源的作用局限于带资源的 `try` 语句。
2. 可以在一条 `try` 语句中声明或初始化多个资源，每个资源以`;`隔开即可。
3. 需要关闭的资源必须实现了 `AutoCloseable` 或 `Closeable` 接口。

> `Closeable` 是 `AutoCloseable` 的子接口，`Closeable` 接口里的 `close()` 方法声明抛出了 `IOException`，因此它的实现类在实现 `close`() 方法时只能声明抛出 `IOException` 或其子类；`AutoCloseable` 接口里的 `close()` 方法声明抛出了 `Exception`，因此它的实现类在实现 `close()` 方法时可以声明抛出任何异常。

如何使用自动关闭资源的 `try` 语句：

```java
public class AutoCloseTest {    
    public static void main(String[] args) throws IOException {        
        try (                
            // 声明、初始化两个可关闭的资源                
            // try语句会自动关闭这两个资源                
            BufferedReader br = new BufferedReader(new FileReader("AutoCloseTest.java"));             PrintStream ps = new PrintStream(new FileOutputStream("a.txt"))) {         
            // 使用两个资源            
            System.out.println(br.readLine());            
            ps.println("OK");        
        }    
    }
}
```

上面程序中分别声明、初始化了两个 IO 流，`BufferedReader` 和 `PrintStream` 都实现了 `Closeable` 接口，并在 `try` 语句中进行了声明和初始化，所以 `try` 语句会自动关闭它们。

自动关闭资源的 `try` 语句相当于包含了隐式的 `finally` 块（这个 `finally` 块用于关闭资源），因此这个 `try` 语句可以既没有 `catch` 块，也没有 `finally` 块。

> Java 7 几乎把所有的“资源类”（包括文件 IO 的各种类、`JDBC` 编程的 `Connection` 和 `Statement` 等接口）进行了改写，改写后的资源类都实现了 `AutoCloseable` 或 `Closeable` 接口。

如果程序需要，自动关闭资源的 `try` 语句后也可以带多个 `catch` 块和一个 `finally` 块。

Java 9 再次增强了这种 `try` 语句。Java 9 不要求在 `try` 后的圆括号内声明并创建资源，只需要自动关闭的资源有 `final` 修饰或者是有效的 `final` (`effectively final`)，Java 9 允许将资源变量放在 `try` 后的圆括号内。

在 Java 9 中可改写为如下形式：

```Java
public class AutoCloseTest {    
    public static void main(String[] args) throws IOException {        
        // 有final修饰的资源        
        final BufferedReader br = new BufferedReader(new FileReader("AutoCloseTest.java"));        
        // 没有显式使用final修饰，但只要不对该变量重新赋值，该变量就是有效的        
        final PrintStream ps = new PrintStream(new FileOutputStream("a. txt"));        
        // 只要将两个资源放在try后的圆括号内即可        
        try (br; ps) {            
            // 使用两个资源            
            System.out.println(br.readLine());            
            ps.println("OK");        
        }    
    }
}
```