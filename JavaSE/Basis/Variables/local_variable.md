# 局部变量(`local variable`)

局部变量是指在方法或者方法代码块中定义的变量。

其作用域是其所在的代码块。可分为以下三种：

- **方法参数变量**(形参)：在整个方法内有效。
- **方法局部变量**(方法内定义)： 从定义这个变量开始到方法结束这一段时间内有效。
- **代码块局部变量**(代码块内定义)：从定义这个变量开始到代码块结束这一段时间内有效。

定义变量的**格式**:

```java
数据类型 变量名 = 变量值;
```

**注意**：

* 局部变量在使用前必须**先声明、初始化(赋初值)再使用**。

* 变量都有其对应的作用域。
  在类中声明的位置：声明在方法内、方法形参、代码块、构造器内部的变量。

* 不可以使用[权限修饰符](../../Advanced/Object_Oriented/Keyword/README.md)。

* 没有默认初始化值 意味着在调用局部变量之前一定要显式赋值。

  ​	特别的 形参在调用时 赋值即可。

* 在内存中加载到栈空间中。

* 方法局部变量或代码块局部变量，生命周期是从声明位置开始到方法或语句执行完毕为止。

## 方法局部变量

声明两个局部变量并输出其值，实现代码如下：

```java
public class Test2 {    
    public static void main(String[] args) {        
        int a = 7;        
        if (5 > 3) {            
            int s = 3; // 声明一个 int 类型的局部变量            
            System.out.println("s=" + s);            
            System.out.println("a=" + a);        
        }        
        System.out.println("a=" + a);    
    }
}
```

上述实例中定义了 a 和 s 两个局部变星，其中 `int` 类型的 a 的作用域是整个 `main()` 方法，而 `int` 类型的变量 s 的作用域是 `if` 语句的代码块内，其执行结果：

![运行结果](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208242117175.png)
如果在 if 方法外调用变量 s，则会报无法解析该变量的错误。

## 方法参数变量

作为方法参数声明的变量的作用域是整个方法。

声明一个方法参数变量，实现代码如下：

```java
public class Test3 {    
    public static void testFun(int n) {        
        System.out.println("n=" + n);    
    }    
    public static void main(String[] args) {        
        testFun(3);    
    }
}
```

在上述实例中定义了一个 `testFun()` 方法，该方法中包含一个 int 类型的参数变量 n，其作用域是 `testFun()` 方法体内。当调用方法时传递进了一个参数 3，因此其输出控制台的 n 值是 3。

## 代码块局部变量

代码块局部变量常用于 `try catch` 代码块中，成为异常处理参数变量。

异常处理参数变量的作用域是在异常处理块中，该变量是将异常处理参数传递给异常处理块，与方法参数变量类似。

声明一个异常处理语句，实现代码如下：

```java
public class Test4 {    
    public static void test() {        
        try {            
            System.out.println("Hello!Exception!");        
        } catch (Exception e) { // 异常处理块，参数为 Exception 类型            
            e.printStackTrace();        
        }    
    }    
    public static void main(String[] args) {        
        test();    
    }
}
```

在上述实例中定义了异常处理语句，异常处理块 `catch` 的参数为 `Exception` 类型的变量 `e`，作用域是整个 `catch` 块。

### 局部变量

在方法内部定义的变量称为局部变量，局部变量作用域从变量声明处开始到对应的块结束。方法参数也是局部变量。

```
package abc;

public class Hello {
    void hi(String name) { // ①
        String s = name.toLowerCase(); // ②
        int len = s.length(); // ③
        if (len < 10) { // ④
            int p = 10 - len; // ⑤
            for (int i=0; i<10; i++) { // ⑥
                System.out.println(); // ⑦
            } // ⑧
        } // ⑨
    } // ⑩
}
```

我们观察上面的`hi()`方法代码：

- 方法参数name是局部变量，它的作用域是整个方法，即①～⑩；
- 变量s的作用域是定义处到方法结束，即②～⑩；
- 变量len的作用域是定义处到方法结束，即③～⑩；
- 变量p的作用域是定义处到if块结束，即⑤～⑨；
- 变量i的作用域是for循环，即⑥～⑧。

使用局部变量时，应该尽可能把局部变量的作用域缩小，尽可能延后声明局部变量。