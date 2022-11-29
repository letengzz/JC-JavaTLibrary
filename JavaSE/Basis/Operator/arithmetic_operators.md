# 算术运算符

Java 中的算术运算符主要用来组织数值类型数据的算术运算。

![图片4](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207291017256.png)

**注意**：

- 算术运算符都是双目运算符，即连接两个操作数的运算符。优先级上，`*`、`/`、`％` 具有相同运算级别，并高于 `+`、`-`（`+`、`-` 具有相同级别）
- 整数的除法对于除数为0时运行时将报错，但编译不会报错。


- `/`运算符取的是商的值，比如int只能取到整数的值，要想取到小数位数要用double或者float，`%` 运算符取的是结果的余数

- 如果对负数取模，可以把模数负号忽略不记，如：`5%-2=1`。 但被模数是负数则不可忽略。此外，取模运算的结果不一定总是整数。 

- 对于除号"`/`"，它的整数除和小数除是有区别的：整数之间做除法时，只保留整数部分而舍弃小数部分。 例如：`int x=3510; x=x/1000*1000;`x的 结果是3000 

- "`+`"除字符串相加功能外，还能把非字符串转换成字符串。

  例如： `System.out.println(“5+5=”+5+5);` //打印结果是 5+5=55 

# 自增/自减

在对一个变量做加 1 或减 1 处理时，可以使用自增运算符 `++` 或自减运算 `--`。`++` 或 `--` 是单目运算符，放在操作数的前面或后面都是允许的。`++` 与 `--` 的作用是使变量的值增 1 或减 1。操作数必须是一个整型或浮点型变量。

```java
// 自增/自减运算
public class Main {
    public static void main(String[] args) {
        int n = 3300;
        n++; // 3301, 相当于 n = n + 1;
        n--; // 3300, 相当于 n = n - 1;
        int y = 100 + (++n); // 不要这么写
        System.out.println(y);
    }
}
```

**注意**：

- `++`写在前面和后面计算结果是不同的，`++n`表示先加1再引用n，`n++`表示先引用n再加1。不建议把`++`运算混入到常规运算中，容易自己把自己搞懵了。

- 自增/自减只能作用于变量，不允许对常量、表达式或其他类型的变量进行操作。常见的错误是试图将自增或自减运算符用于非简单变量表达式中。
- 自增/自减运算可以用于整数类型 byte、short、int、long，浮点类型 float、double，以及字符串类型 char。
- 在 Java 1.5 以上版本中，自增/自减运算可以用于基本类型对应的包装器类 Byte、Short、Integer、Long、Float、Double 和 Character。
- 自增/自减运算结果的类型与被运算的变量类型相同。

```java
public class 算术运算符 {
    public static void main(String[] args) {
        int num1 = 12;
        int num2 = 5;
        int result1 = num1 / num2;
        System.out.println(result1);    //2

        int result2 = num1 / num2 *num2;
        System.out.println(result2);    //10

        double result3 = num1 / num2;
        System.out.println(result3);    //2.0

        double result4 = num1 / num2 +0.0;  //2.0
        double result5 = num1 /(num2 + 0.0);    //2.4
        double result6 = (double) num1 / num2;  //2.4
        double result7 = (double) (num1 / num2);    //2.0

        //%：取余运算
        //结果的符号与被模数符号相同
        int m1 = 12;
        int n1 = 5;
        System.out.println("m1 % n1=" + m1 % n1);   //2
        int m2 = -12;
        int n2 = 5;
        System.out.println("m2 % n2=" + m2 % n2);   //-2
        int m3 = 12;
        int n3 = -5;
        System.out.println("m3 % n3=" + m3 % n3);   //2
        int m4 = -12;
        int n4 = -5;
        System.out.println("m4 % n4=" + m4 % n4);   //-2

        // (前)++:先自增1 后运算
        int a1 = 10;
        int b1 = ++a1;
        System.out.println("a1=" + a1 + "b1=" + b1);    //a1=11b1=11
        // (后)++: 先运算 后自增1
        int a2 = 10;
        int b2 = a2++;
        System.out.println("a2=" + a2 + "b2=" + b2);    //a2=11b2=10

        // (前)--:先自减1 后运算
        // (后)--:先运算 后自减1

        int a3 = 10;
        ++a3;   //a3++
        int b3 = a3;    //两个没有区别 都是独立运算

        //注意点
        short s1 = 10;
        //s1 = s1 +1; //编译失败
        s1 = (short) (s1 + 1);  //正确
        s1++;   //自增1不会改变本身没变量的数据类型

        //问题
        byte bb1 = 127;
        bb1++;
        System.out.println(bb1);    //-128

        //连接符: + 只能使用在String与其他数据类型变量之间使用
    }
}
```

编写一个程序，使用不同类型的数据结合自增和自减运算符进行运算，并输出变量的值：

```java
public static void main(String[] args) {
    int x = 5, y; // 声明用于自增和自减的整型变量
    char cx = 'B', cy; // 声明用于自增和自减的字符型变量
    float fx = 5.5f, fy; // 声明用于自增和自减的浮点型变量
    System.out.println("---------对整数的自增和自减---------");
    y = x++;
    System.out.printf("y=x++ 的结果为：%d ,%d \n", x, y);
    y = x--;
    System.out.printf("y=x-- 的结果为：%d ,%d \n", x, y);
    y = ++x;
    System.out.printf("y=++x 的结果为：%d ,%d \n", x, y);
    y = --x;
    System.out.printf("y=--x 的结果为：%d ,%d \n", x, y);
    System.out.println("\n---------对浮点的自增和自减---------");
    fy = fx++;
    System.out.printf("fy=fx++ 的结果为：%f ,%f \n", fx, fy);
    fy = fx--;
    System.out.printf("fy=fx-- 的结果为：%f ,%f \n", fx, fy);
    fy = ++fx;
    System.out.printf("fy=++fx 的结果为：%f ,%f \n", fx, fy);
    fy = --fx;
    System.out.printf("fy=--fx 的结果为：%f ,%f \n", fx, fy);
    System.out.println("\n---------对字符的自增和自减---------");
    cy = cx++;
    System.out.printf("cy=cx++ 的结果为：%c ,%c \n", cx, cy);
    cy = cx--;
    System.out.printf("cy=cx-- 的结果为：%c ,%c \n", cx, cy);
    cy = ++cx;
    System.out.printf("cy=++cx 的结果为：%c ,%c \n", cx, cy);
    cy = --cx;
    System.out.printf("cy=--cx 的结果为：%c ,%c \n", cx, cy);
}
```

保存代码并运行，输出的结果如下：

> ---------对整数的自增和自减---------
> y=x++ 的结果为：6 ,5
> y=x-- 的结果为：5 ,6
> y=++x 的结果为：6 ,6
> y=--x 的结果为：5 ,5
>
> ---------对浮点的自增和自减---------
> fy=fx++ 的结果为：6.500000 ,5.500000
> fy=fx-- 的结果为：5.500000 ,6.500000
> fy=++fx 的结果为：6.500000 ,6.500000
> fy=--fx 的结果为：5.500000 ,5.500000
>
> ---------对字符的自增和自减---------
> cy=cx++ 的结果为：C ,B
> cy=cx-- 的结果为：B ,C
> cy=++cx 的结果为：C ,C
> cy=--cx 的结果为：B ,B


从运行结果来看，无论是何种类型，只要是自增和自减运算符支持的类型，都可以参与运算。
