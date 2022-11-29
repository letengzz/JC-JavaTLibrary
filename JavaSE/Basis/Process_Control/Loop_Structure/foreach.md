# foreach

 Java 5 之后推出了 for-each 循环语句，for-each 循环是 for 循环的变形，它是**专门为集合遍历而设计的**，。for-each 并不是一个关键字。foreach 循环语句是 for 语句的特殊简化版本，主要用于执行遍历功能的循环。

**语法格式**：

```java
for(类型 变量名:集合) {
    语句块;
}
```

"类型"为集合元素的类型，"变量名"表示集合中的每一个元素，"集合"是被遍历的集合对象或数组。每执行一次循环语句，循环变量就读取集合中的一个元素

**执行流程图**：

![未命名绘图.drawio (2)](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209161606317.png)

假设有一个数组，**采用 for 语句遍历数组的方式**：

```java
// 声明并初始化数组
int[] numbers = { 43, 32, 53, 54, 75, 7, 10 };
System.out.println("----for----");
// for语句
for (int i = 0; i < numbers.length; i++) {    
    System.out.println("Count is:" + numbers[i]);
}
```

第 2 行语句声明并初始化了 7 个元素数组集合。numbers.length 是获得数组的长度，length 是数组的属性，numbers[i] 是通过数组下标访问数组元素。

**采用 for-each 循环语句遍历数组**：

```java 
// 声明并初始化int数组
int[] numbers = { 43, 32, 53, 54, 75, 7, 10 };
System.out.println("----for each----");
// for-each语句
for (int item : numbers) {
    System.out.println("Count is:" + item);
}
```

item 不是循环变量，它保存了集合中的元素，for-each 语句将集合中的元素一一取出来，并保存到 item 中，这个过程中不需要使用循环变量，通过数组下标访问数组中的元素。可见 for-each 语句在遍历集合的时候要简单方便得多。

------

```java 
String[] urls = { "http://baidu,com", "http://google.com"};
// 使用foreach循环来遍历数组元素
// 其中book将会自动迭代每个数组元素
for (String url : urls) {
    System.out.println(url);
}
```

使用 foreach 循环遍历数组元素时无须获得数组长度，也无须根据索引来访问数组元素。

foreach 循环和普通循环不同的是，它无须循环条件，无须循环迭代语句，这些部分都由系统来完成，foreach 循环自动迭代数组的每个元素，当每个元素都被迭代一次后，foreach 循环自动结束。

当使用 foreach 循环来迭代输出数组元素或集合元素时，通常不要对循环变量进行赋值，虽然这种赋值在语法上是允许的，但没有太大的实际意义，而且极容易引起错误。

```java
String[] urls = { "http://www.baidu.com", "http://www.google.com"};
// 使用foreach循环来遍历数组元素，其中 book 将会自动迭代每个数组元素
for (String url : urls) {
    url = "www.abc.com";
    System.out.println(url);
}
System.out.println(urls[0]);
```

运行上边程序：

> www.abc.com
>
> www.abc.com
>
> www.abc.com
>
> http://www.baidu.com

由于在 foreach 循环中对数组元素进行赋值，结果导致不能正确遍历数组元素，不能正确地取出每个数组元素的值。而且当再次访问第一个数组元素时，发现数组元素的值依然没有改变。

不难看出，当使用 foreach 来迭代访问数组元素时，foreach 中的循环变量相当于一个临时变量，系统会把数组元素依次赋给这个临时变量，而这个临时变量并不是数组元素，它只是保存了数组元素的值。因此，如果希望改变数组元素的值，则不能使用这种 foreach 循环。

使用 foreach 循环迭代数组元素时，并不能改变数组元素的值，因此不要对 foreach 的循环变量进行赋值。

**例**：

在一个字符串数组中存储了几种编程语言，现在将这些编程语言遍历输出。

foreach 语句的实现代码：

```Java
public static void main(String[] args) {    
    String[] languages={"Java","ASP.NET","Python","C#","PHP"};    
    System.out.println("现在流行的编程语言有：");    
    // 使用 foreach 循环语句遍历数组    
    for(String lang:languages) {        
        System.out.println(lang);    
    }
}
```

在循环体执行的过程中，每循环一次，会将 languages 数组中的一个元素赋值给 lang 变量，直到遍历 languages 数组中所有元素，循环终止。

该程序运行后的结果：

> 现在流行的编程语言有：
> Java
> ASP.NET
> Python
> C#
> PHP