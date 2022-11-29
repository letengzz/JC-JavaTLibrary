# 隐式准换(自动类型转换)

当容量小的数据类型的变量与容量大的数据类型做运算，结果自动提升为容量大的数据类型

![4](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/4.png)

**满足条件**：

- 两种数据类型彼此兼容
- 目标类型的取值范围大于源数据类型(低级类型数据转换成高级类型数据)

当以上 2 个条件都满足时，拓宽转换(widening conversion)发生。例如 byte 类型向 short 类型转换时，由于 short 类型的取值范围较大，会自动将 byte 转换为 short 类型。

在运算过程中，由于不同的数据类型会转换成同一种数据类型，所以整型、浮点型以及字符型都可以参与混合运算。**自动转换的规则是从低级类型数据转换成高级类型数据**。

**转换规则**：

- 数值型数据的转换：byte→short→int→long→float→double。
- 字符型转换为整型：char→int。

以上数据类型的转换遵循从左到右的转换顺序，最终转换成表达式中表示范围最大的变量的数据类型。

**注意**：

- `byte`，`short`，`char`之间不会相互转换，他们三者在计算时首先转换为`int`类型。`char` 类型比较特殊，`char` 自动转换成 `int`、`long`、`float` 和 `double`，但 `byte` 和 `short` 不能自动转换为 `char`，而且 `char` 也不能自动转换为 `byte` 或 `short`。
- 有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算。
- `boolean`类型不能与其他数据类型运算。
- 当把任何基本数据类型的值和字符串(`String`) 进行连接运算时(`+`)，基本数据类型的值将自动转化为字符串(`String`)类型。

```java
public class 自动类型转换 {
    public static void main(String[] args) {
        byte b1 = 8;
        int i1 = 144;
        //编译不通过
        //byte b2 = b1 + i1;
        int i2 = b1 + i1;
        long l1 = b1 + i1;
        System.out.println(i2); //152

        float f = b1 + i1;
        System.out.println(f);  //152.0

        short s1 = 123;
        double d1 = s1;
        System.out.println(d1); //123.0

        //***************

        char c1 = 'a';//97
        int i3 = 10;
        int i4 = c1 + i3;
        System.out.println(i4);

        short s2 = 10;
        //char c2 = c1 + s2;//编译不通过

        byte b2 = 10;
        //char c3 = c1 + b2;//编译不通过
        //short s3 = b2 + s2;//编译不通过
        //short s4 = b1 + b2;//编译不通过
    }
}
```

当然自动类型提升会引起令人疑惑的编译错误。

**例**：

```java
byte b = 50;
b = b * 2;  // Type mismatch: cannot convert from int to byte
```

第二行会报“类型不匹配：无法从int转换为byte错误。

该程序试图将一个完全合法的 byte 型的值 50*2 再存储给一个 byte 型的变量。但是当表达式求值的时候，操作数被自动的提升为 int 型，计算结果也被提升为 int 型。这样表达式的结果现在是 int 型，不强制转换它就不能被赋为 byte 型。确实如此，在这个特别的情况下，被赋的值将仍然适合目标类型。

应该使用[强制类型转换](type_cast.md)：

```java
byte b = 50;
b = (byte)(b*2);
```

这样就能产生正确的值 100。

