## 三元运算符 

Java 提供了一个特别的三元运算符(也叫三目运算符)经常用于取代某个类型的 `if-then-else` 语句。条件运算符的符号表示为"`?` `:`"，使用该运算符时需要有三个操作数，因此称其为**三目运算符**。

**语法结构**：

```java
(条件表达式) ? 表达式1 : 表达式2
```

**说明：**

- 条件表达式的结果为boolean类型
- 根据条件表达式 决定执行表达式1还是表达式2
  - 如果表达式为true，则执行表达式1
  - 如果表达式为false，则执行表达式2

**注意**：

- 表达式1和表达式2类型要保持一致。

- 三元运算符，可以嵌套。

- 凡是可以使用三元运算符的地方都可以改写成[if-else](../Process_Control/Branch_Structure/if_else.md)；

  用[if-else](../Process_Control/Branch_Structure/if_else.md)的地方不一定可以改写成三元运算符。

- 如果程序既可以使用三元运算符又可以使用[if-else](../Process_Control/Branch_Structure/if_else.md)，那么优先选择三元运算符。

  **原因**： 简洁、执行效率高。

**例**：

1. ```java
   int x,y,z;
   x = 6,y = 2;
   z = x>y ? x-y : x+y;
   ```

   在这里要计算 z 的值，首先要判断 x>y 表达的值，如果为 true，z 的值为 x-y；否则 z 的值为 x+y。很明显 x>y 表达式结果为 true，所以 z 的值为 4。

   **技巧**：可以将条件运算符理解为 if-else 语句的简化形式，在使用较为简单的表达式时，使用该运算符能够简化程序代码，使程序更加易读。

   在使用条件运算符时，还应该注意优先级问题：

   ```java
   x>y ? x-=y : x+=y;
   ```

   在编译时会出现语法错误，因为条件运算符优先于赋值运算符，上面的语句实际等价于：

   ```java
   (x>y ? x-=y : x)+=y;
   ```

   而运算符"`+=`"是赋值运算符，该运算符要求左操作数应该是一个变量，因此出现错误。为了避免这类错误，可以使用括号"`( )`"来加以区分：

   ```java
   (x>y) ? (x-=y): (x+=y);
   ```


2. 在程序中声明 3 个变量 x、y、z，并由用户从键盘输入 x 的值，然后使用条件运算符向变量 y 和变量 z 赋值。 实现代码如下：

   ```java
   public class Test9 {
       public static void main(String[] args) {
           int x, y, z; // 声明三个变量
           System.out.print("请输入一个数：");
           Scanner input = new Scanner(System.in);
           x = input.nextInt(); // 由用户输入x的值
           // 判断x的值是否大于5，如果是y=x，否则y=-x
           y = x > 5 ? x : -x;
           // 判断y的值是否大于x，如果是z=y，否则z=5
           z = y > x ? y : 5;
           System.out.printf("x=%d \n", x);
           System.out.printf("y=%d \n", y);
           System.out.printf("z=%d \n", z);
       }
   }
   ```

   ![键盘输入58](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209141657729.png)

   ![键盘输入4](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209141657611.png)

   在该程序中，首先输入 x 的值为 58，然后判断 x 的值是否大于 5，显然条件是成立，则 y 的值为 x，即 y=58。接着判断 y 的值是否大于 x，因为 y 的值和 x 的值都为 58，所以该条件是不成立的，则 z=5。再次输入 x 的值为 4，然后判断 x 的值是否大于 5，不成立，则 y=-4；接着判断 y 的值是否大于 x，不成立，则 z=5。







