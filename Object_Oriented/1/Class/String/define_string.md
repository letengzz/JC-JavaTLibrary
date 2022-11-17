# 定义String变量

## 直接定义字符串

​	直接定义字符串是指使用双引号表示字符串中的内容，例如“Hello Java”、“Java编程”等。具体方法是用字符串常量直接初始化一个 String 对象。

**注意**：字符串变量必须经过初始化才能使用。

```java
String str = "Hello Java";	//直接赋值
String str;	//先定义String变量
str = "Hello Java";	//赋值
```

## 使用 String 类定义

​	可以通过使用 String 类的构造方法来创建字符串，该类位于 `java.lang` 包中。

​	String 类的构造方法有多种重载形式，每种形式都可以定义字符串。

**注意**：具有和类名相同的名称，而且没有返回类型的方法称为构造方法。重载是指在一个类中定义多个同名的方法，但要求每个方法具有不同的参数的类型或参数的个数。

### String()

​	初始化一个新创建的 String 对象，表示一个空字符序列。

### String(String original)

​	初始化一个新创建的 String 对象，使其表示一个与参数相同的字符序列。换句话说，新创建的字符串是该参数字符串的副本

```java
String str1 = new String("Hello Java");
String str2 = new String(str1);
```

**注意**：这里 str1 和 str2 的值是相等的。

### String(char[ ]value)

​	分配一个新的字符串，将参数中的字符数组元素全部变为字符串。该字符数组的内容已被复制，后续对字符数组的修改不会影响新创建的字符串。

```java
char a[] = {'H','e','l','l','0'};
String sChar = new String(a);
a[1] = 's';
```

**注意**：sChar 变量的值是字符串"Hello"。 即使在创建字符串之后，对 a 数组中的第 2 个元素进行了修改，但未影响 sChar 的值。

#### String(char[] value,int offset,int count)

​	分配一个新的 String，它包含来自该字符数组参数一个子数组的字符。offset 参数是子数组第一个字符的索引，count 参数指定子数组的长度。该子数组的内容已被赋值，后续对字符数组的修改不会影响新创建的字符串。

```java
char a[]={'H','e','l','l','o'};
String sChar=new String(a,1,4);
a[1]='s';
```

**注意**：sChar 变量的值是字符串“ello”。该构造方法使用字符数组中的部分连续元素来创建字符串对象。offset 参数指定起始索引值，count 指定截取元素的个数。创建字符串对象后，即使在后面修改了 a 数组中第 2 个元素的值，对 sChar 的值也没有任何影响。



