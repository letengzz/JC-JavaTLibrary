# `continue`关键字

continue语句 将中断正常的控制流程。continue 语句将控制转移到最内层循环的首部。

continue 语句是跳过循环体中剩余的语句而强制执行下一次循环，其作用为结束本次循环，即跳过循环体中下面尚未执行的语句，接着进行下一次是否执行循环的判定。

continue 语句类似于 break 语句，但它只能出现在循环体中。它与 break 语句的区别在于：continue 并不是中断循环语句，而是中止当前迭代的循环，进入下一次的迭代。简单来讲，continue 是忽略循环语句的当次循环。

**break与continue对比**：

![](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209161610898.png)

**注意**：continue 语句只能用在 while 语句、for 语句或者 foreach 语句的循环体之中，在这之外的任何地方使用它都会引起语法错误。

在循环体中使用 continue 语句有两种方式可以带有标签，也可以不带标签。

**语法格式**：

```java 
continue //不带标签
continue label //带标签，label是标签名
```


下面看一个示例，代码如下：

```java
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
for (int i = 0; i < numbers.length; i++) {    
    if (i == 3) {        
        continue;    
    }    
    System.out.println("Count is: " + i);
}
```

在上述程序代码中，当条件 i==3 的时候执行 continue 语句，continue 语句会终止本次循环，循环体中 continue 之后的语句将不再执行，接着进行下次循环，所以输出结果中没有 3。

运行结果：

> Count is: 0
> Count is: 1
> Count is: 2
> Count is: 4
> Count is: 5
> Count is: 6
> Count is: 7
> Count is: 8
> Count is: 9

带标签的 continue 语句例：

```java
public static void main(String[] args) {    
    label1: for (int x = 0; x < 5; x++) {        
        for (int y = 5; y > 0; y--) {            
            if (y == x) {                
                continue label1;            
            }            
            System.out.println(x+","+y);        
        }    
    }    
    System.out.println("Game Over!");
}
```

默认情况下，continue 只会跳出最近的内循环（代码第 3 行的 for 循环），如果要跳出代码第 2 行的外循环，可以为外循环添加一个标签 label1，然后在第 5 行的 continue 语句后面指定这个标签 label1，这样当条件满足执行 continue 语句时，程序就会跳转出外循环。

程序运行结果：

> 0,5
> 0,4
> 0,3
> 0,2
> 0,1
> 1,5
> 1,4
> 1,3
> 1,2
> 2,5
> 2,4
> 2,3
> 3,5
> 3,4
> 4,5
> Game Over!

由于跳过了 x == y，因此下面的内容没有输出。

> 1,1
> 2,2
> 3,3
> 4,4
