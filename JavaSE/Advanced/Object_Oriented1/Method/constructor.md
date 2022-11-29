# 构造方法

创建实例的时候，经常需要同时初始化这个实例的字段：

```java
Person ming = new Person();
ming.setName("小明");
ming.setAge(12);
```

初始化对象实例需要3行代码，而且，如果忘了调用`setName()`或者`setAge()`，这个实例内部的状态就是不正确的。

构造方法可以在创建对象实例时就把内部字段全部初始化为合适的值。

创建实例的时候，实际上是通过构造方法来初始化实例的。先定义一个构造方法，能在创建`Person`实例的时候，一次性传入`name`和`age`，完成初始化：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Xiao Ming", 15);
        System.out.println(p.getName());
        System.out.println(p.getAge());
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值（也没有`void`），调用构造方法，必须用`new`操作符。

## 默认构造方法

任何`class`都有构造方法。

如果一个类没有定义构造方法，编译器会自动为我们生成一个默认构造方法，它没有参数，也没有执行语句：

```java
class Person {
    public Person() {
    }
}
```

**注意**：如果我们自定义了一个构造方法，那么，编译器就不再自动创建默认构造方法：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person(); // 编译错误:找不到这个构造方法
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

如果既要能使用带参数的构造方法，又想保留不带参数的构造方法，那么只能把两个构造方法都定义出来：

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Xiao Ming", 15); // 既可以调用带参数的构造方法
        Person p2 = new Person(); // 也可以调用无参数构造方法
    }
}

class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

没有在构造方法中初始化字段时，引用类型的字段默认是`null`，数值类型的字段用默认值，`int`类型默认值是`0`，布尔类型默认值是`false`：

```java
class Person {
    private String name; // 默认初始化为null
    private int age; // 默认初始化为0

    public Person() {
    }
}
```

也可以对字段直接进行初始化：

```java
class Person {
    private String name = "Unamed";
    private int age = 10;
}
```

既对字段进行初始化，又在构造方法中对字段进行初始化：

```java
class Person {
    private String name = "Unamed";
    private int age = 10;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

在Java中，创建对象实例的时候，按照如下顺序进行初始化：

1. 先初始化字段，例如，`int age = 10;`表示字段初始化为`10`，`double salary;`表示字段默认初始化为`0`，`String name;`表示引用类型字段默认初始化为`null`；
2. 执行构造方法的代码进行初始化。

因此，构造方法的代码由于后运行，所以，`new Person("Xiao Ming", 12)`的字段值最终由构造方法的代码确定。

## 多构造方法

可以定义多个构造方法，在通过`new`操作符调用的时候，编译器通过构造方法的参数数量、位置和类型自动区分：

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this.name = name;
        this.age = 12;
    }

    public Person() {
    }
}
```

如果调用`new Person("Xiao Ming", 20);`，会自动匹配到构造方法`public Person(String, int)`。

如果调用`new Person("Xiao Ming");`，会自动匹配到构造方法`public Person(String)`。

如果调用`new Person();`，会自动匹配到构造方法`public Person()`。

一个构造方法可以调用其他构造方法，这样做的目的是便于代码复用。调用其他构造方法的语法是`this(…)`：

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this(name, 18); // 调用另一个构造方法Person(String, int)
    }

    public Person() {
        this("Unnamed"); // 调用另一个构造方法Person(String)
    }
}
```

## 总结

- 实例在创建时通过`new`操作符会调用其对应的构造方法，构造方法用于初始化实例。


- 没有定义构造方法时，编译器会自动创建一个默认的无参数构造方法。


- 可以定义多个构造方法，编译器根据参数自动判断。


- 可以在一个构造方法内部调用另一个构造方法，便于代码复用。



构造方法是类的一种特殊方法，用来初始化类的一个新的对象，在创建对象（new 运算符）之后自动调用。[Java](http://c.biancheng.net/java/) 中的每个类都有一个默认的构造方法，并且可以有一个以上的构造方法。

Java 构造方法有以下特点：

- 方法名必须与类名相同
- 可以有 0 个、1 个或多个参数
- 没有任何返回值，包括 void
- 默认返回类型就是对象类型本身
- 只能与 new 运算符结合使用


值得注意的是，如果为构造方法定义了返回值类型或使用 void 声明构造方法没有返回值，编译时不会出错，但 Java 会把这个所谓的构造方法当成普通方法来处理。

这时候大家可能会产生疑问，构造方法不是没有返回值吗？为什么不能用 void 声明呢？

简单的说，这是 Java 的语法规定。实际上，类的构造方法是有返回值的，当使用 new 关键字来调用构造方法时，构造方法返回该类的实例，可以把这个类的实例当成构造器的返回值，因此构造器的返回值类型总是当前类，无须定义返回值类型。但必须注意不要在构造方法里使用 return 来返回当前类的对象，因为构造方法的返回值是隐式的。

注意：构造方法不能被 static、final、synchronized、abstract 和 native（类似于 abstract）修饰。构造方法用于初始化一个新对象，所以用 static 修饰没有意义。构造方法不能被子类继承，所以用 final 和 abstract 修饰没有意义。多个线程不会同时创建内存地址相同的同一个对象，所以用 synchronized 修饰没有必要。如果不了解除 static、final 之外其他的关键字，教程后面会详细讲解。

构造方法的语法格式如下：

```
class class_name {    public class_name(){}    // 默认无参构造方法    public ciass_name([paramList]){}    // 定义构造方法    …    // 类主体}
```

在一个类中，与类名相同的方法就是构造方法。每个类可以具有多个构造方法，但要求它们各自包含不同的方法参数。

#### 例 1

构造方法主要有无参构造方法和有参构造方法两种，示例如下：

```
public class MyClass {    private int m;    // 定义私有变量    MyClass() {        // 定义无参的构造方法        m = 0;    }    MyClass(int m) {        // 定义有参的构造方法        this.m = m;    }}
```

该示例定义了两个构造方法，分别是无参构造方法和有参构造方法。在一个类中定义多个具有不同参数的同名方法，这就是方法的重载。这两个构造方法的名称都与类名相同，均为 MyClass。在实例化该类时可以调用不同的构造方法进行初始化。

注意：类的构造方法不是要求必须定义的。如果在类中没有定义任何一个构造方法，则 Java 会自动为该类生成一个默认的构造方法。默认的构造方法不包含任何参数，并且方法体为空。如果类中显式地定义了一个或多个构造方法，则 Java 不再提供默认构造方法。

提示：无参数的构造方法也被称为 Nullary 构造方法。只有编译程序自动加入的构造方法，才称为默认构造函数。如果自行编写无参数、没有内容的构造函数，就不称为默认构造函数了（只是 Nullary 构造函数）。虽然只是名词定义，不过认证考试时要区别一下两者的不同。

#### 例 2

要在不同的条件下使用不同的初始化行为创建类的对象，这时候就需要在一个类中创建多个构造方法。下面通过一个示例来演示构造方法的使用。

1）首先在员工类 Worker 中定义两个构造方法，代码如下：

```
public class Worker {    public String name;    // 姓名    private int age;    // 年龄    // 定义带有一个参数的构造方法    public Worker(String name) {        this.name = name;    }    // 定义带有两个参数的构造方法    public Worker(String name,int age) {        this.name = name;        this.age = age;    }    public String toString() {        return "大家好！我是新来的员工，我叫"+name+"，今年"+age+"岁。";    }}
```

在 Worker 类中定义了两个属性，其中 name 属性不可改变。分别定义了带有一个参数和带有两个参数的构造方法，并对其属性进行初始化。最后定义了该类的 toString() 方法，返回一条新进员工的介绍语句。

提示：Object 类具有一个 toString() 方法，该方法是个特殊的方法，创建的每个类都会继承该方法，它返回一个 String 类型的字符串。如果一个类中定义了该方法，则在调用该类对象时，将会自动调用该类对象的 toString() 方法返回一个字符串，然后使用“System.out.println(对象名)”就可以将返回的字符串内容打印出来。

2）在 TestWorker 类中创建 main() 方法作为程序的入口处，在 main() 方法中调用不同的构造方法实例化 Worker 对象，并对该对象中的属性进行初始化，代码如下：

```
public class TestWorker {    public static void main(String[] args) {        System.out.println("-----------带有一个参数的构造方法-----------");        // 调用带有一个参数的构造方法        Worker worker1 = new Worker("张强");        System.out.println(worker1);        System.out.println("-----------带有两个参数的构造方法------------");        // 调用带有两个参数的构造方法        Worker worker2 = new Worker("李丽",25);        System.out.println(worker2);    }}
```

在上述代码中，创建了两个不同的 Worker 对象：一个是姓名为张强的员工对象，一个是姓名为李丽、年龄为 25 的员工对象。对于第一个 Worker 对象 Worker1，并未指定 age 属性值，因此程序会将其值采用默认值 0。对于第二个 Worker 对象 Worker2，分别对其指定了 name 属性值和 age 属性值，因此程序会将传递的参数值重新赋值给 Worker 类中的属性值。

注意：Java 构造器的工作方式与 [C++](http://c.biancheng.net/cplus/) 一样。但是，要记住所有的 Java 对象都是在堆中构造的，构造器总是伴随着 new 操作符一起使用。C++ 程序员最易犯的错误就是忘记 new 操作符，例如以下语句：

```
Worker worker("张三",12);
```

这条语句在 C++ 中能够正常运行，但在 Java 中却不行。

运行 TestWorker 类，输出的结果如下：

```
-----------带有一个参数的构造方法-----------
大家好！我是新来的员工，我叫张强，今年0岁。
-----------带有两个参数的构造方法------------
大家好！我是新来的员工，我叫李丽，今年25岁。
```

通过调用带参数的构造方法，在创建对象时，一并完成了对象成员的初始化工作，简化了对象初始化的代码。