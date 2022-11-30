# 整数类型

​	Java各整数类型有固定的表数范围和字段长度,不受具体OS的影响,以保证java程序的可移植性。

​	整数类型: `byte`, `short`, `int`, `long`

![图片1](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207221746703.png)

`bit`：计算机中的最小存储单位。 `byte`：计算机中基本存储单元。

**说明**：

- `byte` 类型是最小的整数类型。当用户从网络或文件中处理数据流时，或者处理可能与 Java 的其他内置类型不直接兼容的未加工的二进制数据时，该类型非常有用。
- `short` 类型限制数据的存储为先高字节，后低字节，这样在某些机器中会出错，因此该类型很少被使用。
- `int` 类型是最常使用的一种整数类型。
- 对于大型程序常会遇到很大的整数，当超出 `int` 类型所表示的范围时就要使用 `long` 类型。

**注意**：

- `byte`恰好就是一个字节，而`long`和`double`需要8个字节。
- **Java的整型常量默认为int型**，当用二进制定义整数时，其32位是符号位；

- 声明long型常量须后加**"`l`"或"`L`"**，二进制默认占64位，第64位是符号位

- Java程序中变量通常声明为int型,除非不足以表示较大的数,才使用long
- 同一个数的不同进制的表示是完全相同的，例如`15`=`0xf`＝`0b1111`
- long类型如果不加`L`的话，那这个整数就是从int类型转向long类型，属于向上转型，在长度不超过int长度时不会报错，如果超过int长度时则会报错。

**整型常量的四种表示形式：**

- **二进制**(`binary`)：`0`、`1`，满二进一，以`0b`或`0B`开头
- **十进制**(`decimal`)：`0~9`，满十进一
- **八进制**(`octal`)：`0~7`，满八进一，以`0`开头表示
- **十六进制**(`hex`)：`0~9`及`A~F`，满十六进一，以`0x`或`0X`开头表示，此处的A-F不区分大小写 如:`0x21AF + 1 = 0X21B0`

```java
public class Main {
    public static void main(String[] args) {
        short s1 = 12;
        
        byte b1 = 12;
        byte b2 = -128;
        
        int i = 2147483647;
        int i2 = -2147483648;
        int i3 = 2_000_000_000; // 加下划线更容易识别
        int i4 = 0xff0000; // 十六进制表示的16711680
        int i5 = 0b1000000000; // 二进制表示的512
        
        long l = 9000000000000000000L; // long型的结尾需要加L
        long l1 = 1212L;
        //编译失败：过大的整数
        //long l2 = 2131334344434;
        long l2 = 2131334344434l;
    }
}
```

# 整数运算相关问题

## 溢出

​	整数由于存在范围限制，如果计算结果超出了范围，就会产生溢出，而溢出不会出错，却会得到一个奇怪的结果：

```java
public class Main {
    public static void main(String[] args) {
        int x = 2147483640;
        int y = 15;
        int sum = x + y;
        System.out.println(sum); // -2147483641
    }
}
```

要解释上述结果，我们把整数`2147483640`和`15`换成二进制做加法：

```ascii
  0111 1111 1111 1111 1111 1111 1111 1000
+ 0000 0000 0000 0000 0000 0000 0000 1111
-----------------------------------------
  1000 0000 0000 0000 0000 0000 0000 0111
```

由于最高位计算结果为`1`，因此，加法结果变成了一个负数。

要解决上面的问题，可以把`int`换成`long`类型，由于`long`可表示的整型范围更大，所以结果就不会溢出：

```java
long x = 2147483640;
long y = 15;
long sum = x + y;
System.out.println(sum); // 2147483655
```

还有一种简写的运算符，即`+=`，`-=`，`*=`，`/=`，它们的使用方法如下：

```java
n += 100; // 3409, 相当于 n = n + 100;
n -= 100; // 3309, 相当于 n = n - 100;
```

## 遵循四则运算规则

Java的整数运算遵循四则运算规则，可以使用任意嵌套的小括号。四则运算规则和初等数学一致。

```java
public class Main {    
    public static void main(String[] args) {        
        int i = (100 + 200) * (99 - 88); // 3300        
        int n = 7 * (5 + (i - 9)); // 23072        
        System.out.println(i);        
        System.out.println(n);    
    } 
}      
```

整数的数值表示不但是精确的，而且整数运算永远是精确的，即使是除法也是精确的，因为两个整数相除只能得到结果的整数部分：

```java
int x = 12345 / 67; // 184              
```

求余运算使用`%`：

```java
int y = 12345 % 67; // 12345÷67的余数是17            
```

**注意**：整数的除法对于除数为0时运行时将报错，但编译不会报错。