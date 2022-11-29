# 显式转换(强制类型转换)

当两种数据类型不兼容，或目标类型的取值范围小于源类型时，自动转换将无法进行，这时就需要进行**强制类型转换**。

自动提升的逆运算，需要使用**强转符**`(` `)`

```java
byte b = (byte)i2;
```

可以将结果强制转型，即将大范围的整数转型为小范围的整数。强制转型使用`(类型)`，例如，将`int`强制转型为`short`：

```
int i = 12345;
short s = (short) i; // 12345
```

**说明**: 此时的容量大小指的是，表示数的范围的大和小 比如 `float` 容量大于`long`

**注意**：

- 超出范围的强制转型会得到错误的结果，原因是转型时，int的两个高位字节直接被扔掉，仅保留了低位的两个字节，因此，强制转型的结果很可能是错的。

  ```java
  public class Main {
      public static void main(String[] args) {
          int i1 = 1234567;
          short s1 = (short) i1; // -10617
          System.out.println(s1);
          int i2 = 12345678;
          short s2 = (short) i2; // 24910
          System.out.println(s2);
      }
  }
  ```

- 强制类型转换可能导致精度损失

- 引用数据类型不能转换为基本类型，同样，基本类型也不能转换为引用类型。


**例**：通常，字符串不能直接转换为基本类型，但通过基本类型对应的包装类则可以实现把字符串转换成基本类型。 

```java
String a = “43”; 
int num1 = Integer.parseInt(a);
```

- `boolean`类型不可以转换为其它的数据类型。

```java
public class 强制类型转换 {
    public static void main(String[] args) {
        double d1 = 123.9;
        //int i1 = d1;//编译不通过
        int i1 = (int)d1;//截断操作
        System.out.println(i1);

        //没有精度损失
        long l1 = 123;
        short s2 = (short) l1;

        //精度损失
        int i2 = 128;
        byte b = (byte)i2;
        System.out.println(b);//-128
    }
}
```

**String强转int**：

```java
String a = “43”; 
int num1 = Integer.parseInt(a);
System.out.println(num1);
```
