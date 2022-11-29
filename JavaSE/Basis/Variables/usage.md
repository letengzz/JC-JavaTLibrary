# 变量的使用

Java定义变量的**格式**：

```java
数据类型  变量名  [=初始值][,变量名 [=初始值]...];
```

**声明变量**：

```java
数据类型 变量名称;
```

```java
int var; 
```

**变量的赋值**：

```java
变量名 = 值;
```

```java
var = 10;
```

 **声明和赋值变量**：

```java
数据类型 变量名 = 初始化值; 
```

```java
int var = 10;
```

**多个同类型的变量可以同时定义或者初始化**，但是多个变量中间要使用逗号分隔，声明结束时用分号分隔：

```java
String username,address,phone,tel;    // 声明多个变量
int num1=12,num2=23,result=35;    // 声明并初始化多个变量
```

**说明：**

- 变量必须先声明，后使用
- 变量都定义在其作用域内，在[作用域](variables_scope.md)有效，出了失效
- 同一作用域内，不可以同时声明两个同名变量
- [局部变量](local_variable.md)需要初值，[成员变量](member_variable.md)不需要，有默认值。

变量标识符的**命名规范**：

- 首字符必须是字母、下划线(`_`)、美元符号(`$`)或者人民币符号(`¥`)。
- 标识符由数字(0~9)、大写字母(A~Z)、小写字母(a~z)、下划线(`_`)、美元符号(`$`)、人民币符号(`¥`)以及所有在十六进制 `0xc0` 前的 ASCII 码组成。
- 不能把[关键字、保留字](../Correlation/keyword.md)作为标识符。
- 标识符的长度没有限制。
- 标识符区分大小写。

**例**：

1. 定义了一个整型`int`类型的变量，名称为`x`，初始值为`1`：

   ```java
   int x = 1;
   ```
   
2. 变量可以重新赋值。例如，对变量`x`，先赋值`100`，再赋值`200`

   观察两次打印的结果：

   ```java
   public class Main {
       public static void main(String[] args) {
           int x = 100; // 定义int类型局部变量x，并赋予初始值100
           System.out.println(x); // 打印该变量的值，观察是否为100
           x = 200; // 重新赋值为200
           System.out.println(x); // 打印该变量的值，观察是否为200
       }
   }
   class Person{
       public int age;	//成员变量
   }
   ```
   
   **注意**：第一次定义变量`x`的时候，需要指定变量类型`int`，因此使用语句`int x = 100;`。而第二次重新赋值的时候，变量`x`已经存在了，不能再重复定义，因此不能指定变量类型`int`，必须使用语句`x = 200;`。

3. 变量不但可以重新赋值，还可以赋值给其他变量：

   ```java
   public class Main {
       public static void main(String[] args) {
           int n = 100; // 定义变量n，同时赋值为100
           System.out.println("n = " + n); // 打印n的值
   
           n = 200; // 变量n赋值为200
           System.out.println("n = " + n); // 打印n的值
   
           int x = n; // 变量x赋值为n（n的值为200，因此赋值后x的值也是200）
           System.out.println("x = " + x); // 打印x的值
   
           x = x + 100; // 变量x赋值为x+100（x的值为200，因此赋值后x的值是200+100=300）
           System.out.println("x = " + x); // 打印x的值
           System.out.println("n = " + n); // 再次打印n的值，n应该是200还是300？
      }
   }
   ```

   执行`int n = 100;`，该语句定义了变量`n`，同时赋值为`100`，因此，JVM在内存中为变量`n`分配一个“存储单元”，填入值`100`：

   ![image-20220722121013700](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207221216455.png)

   执行`n = 200;`时，JVM把`200`写入变量`n`的存储单元，因此，原有的值被覆盖，现在`n`的值为`200`：

   ![image-20220722121027361](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207221216473.png)

   执行`int x = n;`时，定义了一个新的变量`x`，同时对`x`赋值，因此，JVM需要新分配一个存储单元给变量`x`，并写入和变量`n`一样的值，结果是变量`x`的值也变为`200`：

   ![image-20220722121045191](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207221216940.png)

   执行`x = x + 100;`时，JVM首先计算等式右边的值`x + 100`，结果为`300`（因为此刻`x`的值为`200`），然后，将结果`300`写入`x`的存储单元，因此，变量`x`最终的值变为`300`：

   ![image-20220722121106695](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207221216736.png)

   变量可以反复赋值。注意，等号`=`是赋值语句，不是数学意义上的相等，否则无法解释`x = x + 100`。

