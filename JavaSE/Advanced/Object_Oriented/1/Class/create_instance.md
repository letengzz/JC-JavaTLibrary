# 创建实例

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

![image-20220729192809119](D:/Data/typora/photo/image-20220729192809119.png)

**注意**：

- `Person ming`是定义`Person`类型的变量`ming`，而`new Person()`是创建`Person`实例。
- 两个`instance`拥有`class`定义的`name`和`age`字段，且各自都有一份独立的数据，互不干扰。
-  一个Java源文件可以包含多个类的定义，但只能定义一个public类，且public类名必须与文件名一致。如果要定义多个public类，必须拆到多个Java源文件中。

```Java
public class Main{
    public static void main(String[] args){
        Person person = new Person();	//创建实例
        person.name = "小明";	// 对字段name赋值
        person.age = 25;	// 对字段age赋值
        System.out.println(person.name+"的年龄是"+person.age);	//访问字段
    }
}
class Person{	//Per
    public String name;	//name成员变量
    public int age;	//age成员变量
}
```

