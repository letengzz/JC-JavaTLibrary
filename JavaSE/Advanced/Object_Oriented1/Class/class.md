# class类和对象(包括[String关键字](../../../Basis/Reference_Types/Class/String/README.md))

在面向对象中，类和对象是最基本、最重要的组成单元。类实际上是表示一个客观世界某类群体的一些基本特征抽象。对象就是表示一个个具体的东西。所以说**类是对象的抽象，对象是类的具体**。

现实世界中，我们定义了“人”这种抽象概念，而具体的人则是“小明”、“小红”、“小军”等一个个具体的人。所以，“人”可以定义为一个类（class），而具体的人则是实例（instance）：

| 现实世界 | 计算机模型  | Java代码                   |
| :------- | :---------- | :------------------------- |
| 人       | 类 / class  | class Person { }           |
| 小明     | 实例 / ming | Person ming = new Person() |
| 小红     | 实例 / hong | Person hong = new Person() |
| 小军     | 实例 / jun  | Person jun = new Person()  |

## 类名要求

**注意**：

- 类名必须以英文字母开头，后接字母，数字和下划线的组合。

- 习惯以大写字母开头。

- 要注意遵守命名习惯，好的类命名：

  - `Hello`

  - `NoteBook`

  - `VRPlayer`

- 不好的类命名：

  - `hello`

  - `Good123`

  - `Note_Book`

  - `_World`

## 定义类

因为Java是面向对象的语言，一个程序的基本单位就是`class`，`class`是关键字。

**基本语法**：

```java
class 类名 { 
    //定义字段和方法
} 
```

**例**：

```java
public class Person { // 类名是Person
    public String name;	//name字段
    public int age;	//age字段
    // ...
} // class定义结束
```

一个class可以包含多个字段field(Java中也可以叫Method方法)，字段用来描述一个类的特征。上面的Person类，我们定义了两个字段，一个是String类型的字段，命名为name，一个是int类型的字段，命名为age。因此，通过`class`，把一组数据汇集到一个对象上，实现了数据封装。

**注意**：

- public是[访问修饰符]()，表示该class是公开的，可以被外部访问。不写public，也能正确编译，但是这个类将无法从命令行执行。

- 一个Java源文件可以包含多个类的定义，但只能定义一个public类，且public类名必须与文件名一致。如果要定义多个public类，必须拆到多个Java源文件中。

### 定义属性

属性(成员变量、field字段)是类的组成部分之一。属性通常为基本数据类型，也可以是引用数据类型。

#### 属性的定义

属性用于定义该类或该类对象包含的数据或者说静态特征。属性作用范围是整个类体。

**基本语法**：

```java
访问修饰符 数据类型 属性名 [= 默认值];
```

属性若不赋默认值，则会有默认值：

![](D:/Data/typora/photo/%E5%9B%BE%E7%89%8731.png)

#### 属性的使用

**基本语法**：

```java
对象名.属性名;
```

### 定义方法





## 创建对象(实例)

定义了class，只是定义了对象模版，而要根据对象模版创建出真正的对象实例，必须用new操作符。

new操作符可以创建一个实例，然后，我们需要定义一个引用类型的变量来指向这个实例。

创建了一个Person类型的实例，并通过变量`ming`指向它：

```java
Person ming = new Person();
```

有了指向这个实例的变量，我们就可以通过这个变量来操作实例。访问实例变量可以用`变量.字段`

```java
ming.name = "Xiao Ming"; // 对字段name赋值
ming.age = 12; // 对字段age赋值
System.out.println(ming.name); // 访问字段name

Person hong = new Person();
hong.name = "Xiao Hong";
hong.age = 15;
```

**在内存中的结构**：

![image-20220729192809119](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/image-20220729192809119.png)

**注意**：

- `Person ming`是定义`Person`类型的变量`ming`，而`new Person()`是创建`Person`实例。
- 两个`instance`拥有`class`定义的`name`和`age`字段，且各自都有一份独立的数据，互不干扰。
- 一个Java源文件可以包含多个类的定义，但只能定义一个public类，且public类名必须与文件名一致。如果要定义多个public类，必须拆到多个Java源文件中。

```Java
public class Main{
    public static void main(String[] args){
        Person person = new Person();	//创建实例
        person.name = "小明";	// 对字段name赋值
        person.age = 25;	// 对字段age赋值
        System.out.println(person.name+"的年龄是"+person.age);	//访问字段
    }
}
class Person{	//Person
    public String name;	//name成员变量
    public int age;	//age成员变量
}
```

## 总结

- 在OOP中，`class`和`instance`是“模版”和“实例”的关系。

- 定义`class`就是定义了一种数据类型，对应的`instance`是这种数据类型的实例。

- `class`定义的`field`，在每个`instance`都会拥有各自的`field`，且互不干扰。

- 通过`new`操作符创建新的`instance`，然后用变量指向它，即可通过变量来引用这个`instance`。

- 访问实例字段的方法是`变量名.字段名`；指向`instance`的变量都是引用变量。









