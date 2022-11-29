# String和int的相互转换

# String强转int

```java
String a = “43”; 
int num1 = Integer.parseInt(a);
System.out.println(num1);int num1 = Integer.parseInt(str1); 
System.out.println(num1);   
```



## String转换为int

String 字符串转整型 int 有以下两种方式：

- Integer.parseInt(str)
- Integer.valueOf(str).intValue()

注意：Integer 是一个类，是 int 基本数据类型的封装类。在《[Java Integer类](http://c.biancheng.net/view/890.html)》一节中我们会详细讲解。

例如下面代码所示：

```
public static void main(String[] args) {    String str = "123";    int n = 0;    // 第一种转换方法：Integer.parseInt(str)    n = Integer.parseInt(str);    System.out.println("Integer.parseInt(str) : " + n);    // 第二种转换方法：Integer.valueOf(str).intValue()    n = 0;    n = Integer.valueOf(str).intValue();    System.out.println("Integer.parseInt(str) : " + n);}
```

输出结果为：

Integer.parseInt(str) : 123
Integer.parseInt(str) : 123

在 String 转换 int 时，String 的值一定是整数，否则会报数字转换异常（java.lang.NumberFormatException）。

## int转换为String

整型 int 转 String 字符串类型有以下 3 种方法：

- String s = String.valueOf(i);
- String s = Integer.toString(i);
- String s = "" + i;


例如下面代码所示：

```
public static void main(String[] args) {    int num = 10;    // 第一种方法：String.valueOf(i);    num = 10;    String str = String.valueOf(num);    System.out.println("str:" + str);    // 第二种方法：Integer.toString(i);    num = 10;    String str2 = Integer.toString(num);    System.out.println("str2:" + str2);    // 第三种方法："" + i;    String str3 = num + "";    System.out.println("str3:" + str3);}
```

输出结果为：

str:10
str2:10
str3:10

使用第三种方法相对第一第二种耗时比较大。在使用第一种 valueOf() 方法时，注意 valueOf 括号中的值不能为空，否则会报空指针异常（NullPointerException）。

## valueOf() 、parse()和toString()

#### 1）valueOf()

valueOf() 方法将数据的内部格式转换为可读的形式。它是一种静态方法，对于所有 [Java](http://c.biancheng.net/java/) 内置的类型，在字符串内被重载，以便每一种类型都能被转换成字符串。valueOf() 方法还被类型 Object 重载，所以创建的任何形式类的对象也可被用作一个参数。这里是它的几种形式：

static String valueOf(double num)
static String valueOf(long num)
static String valueOf(Object ob)
static String valueOf(char chars[])

与前面的讨论一样，调用 valueOf() 方法可以得到其他类型数据的字符串形式——例如在进行连接操作时。对各种数据类型，可以直接调用这种方法得到合理的字符串形式。所有的简单类型数据转换成相应于它们的普通字符串形式。任何传递给 valueOf() 方法的对象都将返回对象的 toString() 方法调用的结果。事实上，也可以通过直接调用 toString() 方法而得到相同的结果。

对大多数数组，valueOf() 方法返回一个相当晦涩的字符串，这说明它是一个某种类型的数组。然而对于字符数组，它创建一个包含了字符数组中的字符的字符串对象。valueOf() 方法有一种特定形式允许指定字符数组的一个子集。

它具有如下的一般形式：

static String valueOf(char chars[ ], int startIndex, int numChars)

这里 chars 是存放字符的数组，startIndex 是字符数组中期望得到的子字符串的首字符下标，numChars 指定子字符串的长度。

#### 2）parse()

parseXxx(String) 这种形式，是指把字符串转换为数值型，其中 Xxx 对应不同的数据类型，然后转换为 Xxx 指定的类型，如 int 型和 float 型。

#### 3）toString()

toString() 可以把一个引用类型转换为 String 字符串类型，是 sun 公司开发 Java 的时候为了方便所有类的字符串操作而特意加入的一个方法。
