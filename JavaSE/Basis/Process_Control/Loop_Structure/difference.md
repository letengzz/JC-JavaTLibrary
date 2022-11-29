# for、while和do-while之间的区别

for 循环和 while、do while 循环**不同点**：

由于 while、do while 循环的循环迭代语句紧跟着循环体，因此如果循环体不能完全执行，如使用 continue 语句来结束本次循环，则循环迭代语句不会被执行。但 for 循环的循环迭代语句并没有与循环体放在一起，因此不管是否使用 continue 语句来结束本次循环，循环迭代语句一样会获得执行。

![](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209161604969.png)

**例**：

分别用 for、do-while 和 while 求出 1-10 的和。

**使用for循环**：

```java
public static void main(String[] args) {    
    int sum = 0;    
    for (int i = 1; i < 11; i++) {        
    sum = sum + i;    
    }    
    System.out.println(sum);
}
```

运行结果：

>  55

**使用 do-while 循环**：

```java
public static void main(String[] args) {    
    int sum = 0;    
    int i = 1;    
    do {        
        sum = sum + i;        
        i++;    
    } while (i < 11);    
    System.out.println(sum);
}
```

运行结果为：

> 55

**使用 while 循环**：

```java
public static void main(String[] args) {    
    int sum = 0;    
    int i = 1;    
    while (i < 11) {        
        sum = sum + i;        
        i++;    
    }    
    System.out.println(sum);
}
```

运行结果：

> 55

从上边代码可以看出 for 语句明显更加简练，因为知道循环次数。 