# 包装类

- [装箱和拆箱]()
- []()

在 [Java](http://c.biancheng.net/java/) 的设计中提倡一种思想，即一切皆对象。但是从数据类型的划分中，我们知道 Java 中的数据类型分为基本数据类型和引用数据类型，但是基本数据类型怎么能够称为对象呢？于是 Java 为每种基本数据类型分别设计了对应的类，称之为包装类（Wrapper Classes），也有地方称为外覆类或数据类型类。

包装类和基本数据类型的关系如下表所示。



| 序号 | 基本数据类型 | 包装类    |
| ---- | ------------ | --------- |
| 1    | byte         | Byte      |
| 2    | short        | Short     |
| 3    | int          | Integer   |
| 4    | long         | Long      |
| 5    | char         | Character |
| 6    | float        | Float     |
| 7    | double       | Double    |
| 8    | boolean      | Boolean   |

从上表中我们可以看出，除了 Integer 和 Character 定义的名称与基本数据类型定义的名称相差较大外，其它的 6 种类型的名称都是很好掌握的。

## 装箱和拆箱

在了解包装类后，下面介绍包装类的装箱与拆箱的概念。其实这两个概念本身并不难理解，基本数据类型转换为包装类的过程称为装箱，例如把 int 包装成 Integer 类的对象；包装类变为基本数据类型的过程称为拆箱，例如把 Integer 类的对象重新简化为 int。

手动实例化一个包装类称为手动拆箱装箱。Java 1.5 版本之前必须手动拆箱装箱，之后可以自动拆箱装箱，也就是在进行基本数据类型和对应的包装类转换时，系统将自动进行装箱及拆箱操作，不用在进行手工操作，为开发者提供了更多的方便。例如：

```
public class Demo {    public static void main(String[] args) {        int m = 500;        Integer obj = m;  // 自动装箱        int n = obj;  // 自动拆箱        System.out.println("n = " + n);              Integer obj1 = 500;        System.out.println("obj等价于obj1返回结果为" + obj.equals(obj1));    }}
```

运行结果：

n = 500
obj等价于obj1返回结果为true

自动拆箱装箱是常用的一个功能，读者需要重点掌握。

## 包装类的应用

下面我们讲解 8 个包装类的使用，下面是常见的应用场景。

#### 1) 实现 int 和 Integer 的相互转换

可以通过 Integer 类的构造方法将 int 装箱，通过 Integer 类的 intValue 方法将 Integer 拆箱。例如：

```
public class Demo {    public static void main(String[] args) {        int m = 500;        Integer obj = new Integer(m);  // 手动装箱        int n = obj.intValue();  // 手动拆箱        System.out.println("n = " + n);               Integer obj1 = new Integer(500);        System.out.println("obj等价于obj1的返回结果为" + obj.equals(obj1));    }}
```

运行结果：

n = 500
obj等价于obj1的返回结果为true

#### 2) 将字符串转换为数值类型

在 Integer 和 Float 类中分别提供了以下两种方法：

① Integer 类（String 转 int 型）

```
int parseInt(String s);
```

s 为要转换的字符串。

② Float 类（String 转 float 型）

```
float parseFloat(String s)
```

注意：使用以上两种方法时，字符串中的数据必须由数字组成，否则转换时会出现程序错误。

下面为字符串转换为数值类型的例子：

```
public class Demo {    public static void main(String[] args) {        String str1 = "30";        String str2 = "30.3";        // 将字符串变为int型        int x = Integer.parseInt(str1);        // 将字符串变为float型        float f = Float.parseFloat(str2);        System.out.println("x = " + x + "；f = " + f);    }}
```

运行结果：

x = 30；f = 30.3

#### 3) 将整数转换为字符串

Integer 类有一个静态的 toString() 方法，可以将整数转换为字符串。例如：

```
public class Demo {    public static void main(String[] args) {        int m = 500;        String s = Integer.toString(m);        System.out.println("s = " + s);    }}
```

运行结果：

s = 500