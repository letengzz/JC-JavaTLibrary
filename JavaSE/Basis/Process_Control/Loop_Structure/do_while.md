# do-while循环

do-while 循环语句也是 Java 中运用广泛的循环语句，它由**循环条件**和**循环体**组成，但它与 while 语句略有不同。

do-while 循环语句的特点：**先执行循环体，然后判断循环条件是否成立**。

**基本结构**：

```java
①
do{
	③;
	④;
}while(②);
```

**do-while循环四要素**：

​	①初始化条件

​	②循环条件(boolean 类型)

​	③循环体

​	④迭代条件

**执行过程**：①-③-④-②-③-④-。。。-②

**说明**：首先执行一次循环操作，然后再判断 while 后面的条件表达式是否为 true，如果循环条件满足，循环继续执行，否则退出循环。while 语句后必须以分号表示循环结束。

**注意**：

- do-while 循环至少执行一次循环体

```java
public class DoWhileLoop { 
    public static void main(String args[]) { 
        int result = 0, i = 1; 
        do { 
            result += i; 
            i++; 
            } while (i <= 100); 
    System.out.println("result=" + result); 
    } 
}
```
