# 类和对象概述

**类是描述了一组有相同特性（属性）和相同行为（方法）的一组对象的集合**。

对象或实体所拥有的特征在类中表示时称为**类的属性**。例如，每个人都具有姓名、年龄和体重，这是所有人共有的特征。但是每一个对象的属性值又各不相同，例如，小明和小红都具有体重这个属性，但是他们的体重值是不同的。

对象执行的操作称为**类的方法**。比如，“人”这个对象都具有的行为是“吃饭”，因此，吃饭就是“人”类的一个方法。

综上所述，**类是描述实体的"模板"和"原型"**，它定义了属于这个类的对象所应该具有的状态和行为。比如一名学生在上课。一名正在上课的学生是类，它定义的信息有：姓名、上课。

使用该类定义的不同姓名的人在上课是对象，他们可能是小明、小红、小丽、张会等。在 Java 面向对象编程中，用自定义的类模型可以创建该类的一个实例，也就是对象。

类是实体对象的概念模型，因此通常是笼统的、不具体的。

**类是 Java 中的一种重要的引用数据类型，也是组成 Java 程序的基本要素，因为所有的 Java 程序都是基于类的**。

**例**：

面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。

| 类   | 对象                                       |
| ---- | ------------------------------------------ |
| 人   | 正在清洁的环卫工人小刘、教室里的学生张丽   |
| 汽车 | 一辆黄色的宝马跑车、一辆白色的林肯轿车     |
| 动物 | 一只叫“猫咪”的小花猫、一只叫“欢欢”的贵宾犬 |

| 现实世界 | 计算机模型        | Java代码                   |
| :------- | :---------------- | :------------------------- |
| 人       | 类 / class        | class Person { }           |
| 小明     | 实例(对象) / ming | Person ming = new Person() |
| 小红     | 实例(对象) / hong | Person hong = new Person() |
| 小军     | 实例(对象) / jun  | Person jun = new Person()  |

| 现实世界     | 计算机模型   | Java代码                |
| :----------- | :----------- | :---------------------- |
| 书           | 类 / class   | class Book { }          |
| Java核心技术 | 实例 / book1 | Book book1 = new Book() |
| Java编程思想 | 实例 / book2 | Book book2 = new Book() |
| Java学习笔记 | 实例 / book3 | Book book3 = new Book() |

**类是构造面向对象程序的基本单位**，是抽取了同类对象的共同属性和方法所形成的对象或实体的“模板”。而对象是现实世界中实体的描述，对象要创建才存在，有了对象才能对对象进行操作。类是对象的模板，对象是类的实例。

## class和instance

class是一种对象模版，它定义了如何创建实例，因此，class本身就是一种数据类型：

![class](https://www.liaoxuefeng.com/files/attachments/1260571618658976/l)

而instance是对象实例，instance是根据class创建的实例，可以创建多个instance，每个instance类型相同，但各自属性可能不相同：

![instances](https://www.liaoxuefeng.com/files/attachments/1260571718581056/l)

## 定义class

在Java中，创建一个类，例如，给这个类命名为`Person`，就是定义一个`class`：

```java
class Person {
    public String name;
    public int age;
}
```

一个`class`可以包含多个字段（`field`），字段用来描述一个类的特征。上面的`Person`类，我们定义了两个字段，一个是`String`类型的字段，命名为`name`，一个是`int`类型的字段，命名为`age`。因此，通过`class`，把一组数据汇集到一个对象上，实现了数据封装。

`public`是用来修饰字段的，它表示这个字段可以被外部访问。

## 创建实例

定义了class，只是定义了对象模版，而要根据对象模版创建出真正的对象实例，必须用new操作符。

new操作符可以创建一个实例，然后，我们需要定义一个引用类型的变量来指向这个实例：

```java
Person ming = new Person();
```

上述代码创建了一个Person类型的实例，并通过变量`ming`指向它。

**注意**：区分`Person ming`是定义`Person`类型的变量`ming`，而`new Person()`是创建`Person`实例。

有了指向这个实例的变量，我们就可以通过这个变量来操作实例。访问实例变量可以用`变量.字段`，例如：

```java
ming.name = "Xiao Ming"; // 对字段name赋值
ming.age = 12; // 对字段age赋值
System.out.println(ming.name); // 访问字段name

Person hong = new Person();
hong.name = "Xiao Hong";
hong.age = 15;
```

上述两个变量分别指向两个不同的实例，它们在内存中的结构：

![image-20221019110627843](D:/Data/typora/photo/image-20221019110627843.png)

两个`instance`拥有`class`定义的`name`和`age`字段，且各自都有一份独立的数据，互不干扰。

**注意**：一个Java源文件可以包含多个类的定义，但只能定义一个public类，且public类名必须与文件名一致。如果要定义多个public类，必须拆到多个Java源文件中。



