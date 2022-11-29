# switch-case

switch 语句则用于对多个整型值进行匹配，从而实现分支控制。

switch 语句提供了 if 语句的一个变通形式，可以从多个语句块中选择其中的一个执行。

**基本语法**：

```java
switch(表达式){
  case 常量1;
  	执行语句1;
     //break;
  case 常量2;
     执行语句2
     //break;
  default:
     执行语句n;
     //break;
 }
```

**执行过程**：表达式的值与每个 case 语句中的常量作比较。如果发现了一个与之相匹配的，则执行该 case 语句后的代码。如果没有一个 case 常量与表达式的值相匹配，则执行 default 语句。当然，default 语句是可选的。如果没有相匹配的 case 语句，也没有 default 语句，则什么也不执行。

**说明**：

1. 根据switch 表达式中的值，依次匹配各个case中的常量，一旦匹配成功，则进入相应的case结构中调用其执行语句。
 当调用完执行语句以后，则仍然继续向下执行其他case结构中的执行语句，直到遇到break关键字或此switch-case结构末尾结束为止。

2. [break]()可以使用在 switch-case结构中，表示一旦执行此关键字就跳出switch-case结构中。
3. switch 结构中的表达式 只能是如下6种类型 `byte`、`short`、`char`、`int`、枚举类型`(jdk5.0)`、String类型(Java7 增强了 switch 语句的功能，允许 switch 语句的控制表达式是 `java.lang.String` 类型的变量或表达式。只能是 `java.lang.String` 类型，不能是 `StringBuffer` 或 `StringBuilder` 这两种字符串的类型。)

4. case之后**只能声明常量，不能声明范围**
5. break关键字**是可选的**
6. default **相当于else**，其他情况都不满足则
   default 可选的，位置是灵活的。如果switch case 结构中的多个case的执行语句相同，则可以考虑进行合并

**注意**：

- 凡是使用switch-case的结构，都可以转换为if-else，反之不成立。

- 当写分支结构时，既可以`if-else`又可以`switch-case`(case不太多)优先选择`switch-case`

  原因：switch-case 执行效率稍高。

- 如果在 case 分支语句的末尾没有 [break 语句]()，有可能触发多个 case 分支。那么就会接着执行下一个 case 分支语句。这种情况相当危险，常常会引发错误。

  如果你喜欢 switch 语句，编译代码时可以考虑加上 `-Xlint:fallthrough` 选项：

  `javac -Xlint:fallthrough Test.java`

  这样如果某个分支最后缺少一个 break 语句，编译器就会给出一个警告消息。

**例**：编写一个 Java 程序，根据当前的星期数字输出对应的汉字。在这里使用包含 break 的 switch 语句来判断当前的星期：

```java
public static void main(String[] args) {
    String weekDate = "";
    Calendar calendar = Calendar.getInstance();  // 获取当前时间
    int week = calendar.get(Calendar.DAY_OF_WEEK) - 1;  // 获取星期的第几日
    switch (week) {
        case 0:
            weekDate = "星期日";
            break;
        case 1:
            weekDate = "星期一";
            break;
        case 2:
            weekDate = "星期二";
            break;
        case 3:
            weekDate = "星期三";
            break;
        case 4:
            weekDate = "星期四";
            break;
        case 5:
            weekDate = "星期五";
            break;
        case 6:
            weekDate = "星期六";
            break;
    }
    System.out.println("今天是 " + weekDate);
}
```

首先获取当前的星期值，然后使用 switch 语句判断 week 的值：0 表示星期日，1 表示星期一，2 表示星期二……以此类推，6 表示星期六。只要 week 值与 case 值相符合，则程序将执行该 case 中的语句，并跳出 switch 语句，输出结果。

运行程序，输出的结果：

> 今天是星期五

# 嵌套switch

可以将一个 switch 语句作为一个外部 switch 语句的语句序列的一部分，这称为**嵌套 switch** 语句。因为一个 switch 语句定义了自己的块，外部 switch 语句和内部 switch 语句的 case 常量不会产生冲突。

**例**：

```java
public static void main(String[] args) {    
    switch (count) {        
        case 1:            
            switch (target) {            
                case 0:                
                    System.out.println("target is zero");                
                    break;            
                case 1:                
                    System.out.println("target is one");                
                    break;            
            }            
            break;        
        case 2: // ...    
    }
}
```

内部 switch 语句中的`case 1：`语句与外部 switch 语句中的`case 1：`语句不冲突。变量 count 仅与外层的 case 语句相比较。如果变量 count 为 1，则变量 target 与内层的 case 语句相比较。

# 注意

- switch 语句不同于 if 语句的是 switch 语句仅能测试相等的情况，而 if 语句可计算任何类型的布尔表达式。也就是 switch 语句只能寻找 case 常量间某个值与表达式的值相匹配。
- 在同一个 switch 语句中没有两个相同的 case 常量。当然，外部 switch 语句中的 case 常量可以和内部 switch 语句中的 case 常量相同。
- switch 语句通常比一系列嵌套 if 语句更有效。

当编译一个 switch 语句时，Java 编译器将检查每个 case 常量并且创造一个“跳转表”，这个表将用来在表达式值的基础上选择执行路径。因此，如果你需要在一组值中做出选择，switch 语句将比与之等效的 if-else 语句快得多。

编译器可以这样做是因为它知道 case 常量都是同类型的，所要做的只是将它与 switch 表达式相比较看是否相等。对于一系列的 if 表达式，编译器就无此功能。



