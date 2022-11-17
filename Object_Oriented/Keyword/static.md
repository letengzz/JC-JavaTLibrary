# 静态

在一个`class`中定义的字段，我们称之为实例字段。实例字段的特点是，每个实例都有独立的字段，各个实例的同名字段互不影响。

还有一种字段，是用`static`修饰的字段，称为静态字段：`static field`。

实例字段在每个实例中都有自己的一个独立“空间”，但是静态字段只有一个共享“空间”，所有实例都会共享该字段。举个例子：

```
class Person {
    public String name;
    public int age;
    // 定义静态字段number:
    public static int number;
}
```

我们来看看下面的代码：

```
// static field
```

 Run

对于静态字段，无论修改哪个实例的静态字段，效果都是一样的：所有实例的静态字段都被修改了，原因是静态字段并不属于实例：

```ascii
        ┌──────────────────┐
ming ──>│Person instance   │
        ├──────────────────┤
        │name = "Xiao Ming"│
        │age = 12          │
        │number ───────────┼──┐    ┌─────────────┐
        └──────────────────┘  │    │Person class │
                              │    ├─────────────┤
                              ├───>│number = 99  │
        ┌──────────────────┐  │    └─────────────┘
hong ──>│Person instance   │  │
        ├──────────────────┤  │
        │name = "Xiao Hong"│  │
        │age = 15          │  │
        │number ───────────┼──┘
        └──────────────────┘
```

虽然实例可以访问静态字段，但是它们指向的其实都是`Person class`的静态字段。所以，所有实例共享一个静态字段。

因此，不推荐用`实例变量.静态字段`去访问静态字段，因为在Java程序中，实例对象并没有静态字段。在代码中，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为`类名.静态字段`来访问静态对象。

推荐用类名来访问静态字段。可以把静态字段理解为描述`class`本身的字段（非实例字段）。对于上面的代码，更好的写法是：

```
Person.number = 99;
System.out.println(Person.number);
```

### 静态方法

有静态字段，就有静态方法。用`static`修饰的方法称为静态方法。

调用实例方法必须通过一个实例变量，而调用静态方法则不需要实例变量，通过类名就可以调用。静态方法类似其它编程语言的函数。例如：

```
// static method
```

 Run

因为静态方法属于`class`而不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。

通过实例变量也可以调用静态方法，但这只是编译器自动帮我们把实例改写成类名而已。

通常情况下，通过实例变量访问静态字段和静态方法，会得到一个编译警告。

静态方法经常用于工具类。例如：

- Arrays.sort()
- Math.random()

静态方法也经常用于辅助方法。注意到Java程序的入口`main()`也是静态方法。

### 接口的静态字段

因为`interface`是一个纯抽象类，所以它不能定义实例字段。但是，`interface`是可以有静态字段的，并且静态字段必须为`final`类型：

```
public interface Person {
    public static final int MALE = 1;
    public static final int FEMALE = 2;
}
```

实际上，因为`interface`的字段只能是`public static final`类型，所以我们可以把这些修饰符都去掉，上述代码可以简写为：

```
public interface Person {
    // 编译器会自动加上public statc final:
    int MALE = 1;
    int FEMALE = 2;
}
```

编译器会自动把该字段变为`public static final`类型。

### 练习

给Person类增加一个静态字段count和静态方法getCount，统计实例创建的个数。

从[![img](data:image/png;base64,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)](https://gitee.com/)下载练习：[静态字段和静态方法](https://gitee.com/liaoxuefeng/learn-java/blob/master/practices/Java教程/20.面向对象编程.1255943520012800/10.面向对象基础.1260451488854880/80.静态字段和方法.1260464690677856/oop-static.zip?utm_source=blog_lxf) （推荐使用[IDE练习插件](https://www.liaoxuefeng.com/wiki/1252599548343744/1266092093733664)快速下载）

### 小结

- 静态字段属于所有实例“共享”的字段，实际上是属于`class`的字段；
- 调用静态方法不需要实例，无法访问`this`，但可以访问静态字段和其他静态方法；
- 静态方法常用于工具类和辅助方法。

## 修饰变量

## 修饰方法

## 修饰代码块

## 修饰类

# import static静态导入

在 JDK 1.5 之后增加了一种静态导入的语法，用于导入指定类的某个静态成员变量、方法或全部的静态成员变量、方法。如果一个类中的方法全部是使用 static 声明的静态方法，则在导入时就可以直接使用 import static 的方式导入。

静态导入使用 import static 语句，静态导入也有两种语法，分别用于导入指定类的单个静态成员变量、方法和全部静态成员变量、方法，其中导入指定类的单个静态成员变量、方法的语法格式如下：

```
import static package.ClassName.fieldName|methodName;
```

上面语法导入 package.ClassName 类中名为 fieldName 的静态成员变量或者名为 methodName 的静态方法。例如，可以使用`import static java.lang.System.out;`语句来导入 java.lang.System 类的 out 静态成员变量。

导入指定类的全部静态成员变量、方法的语法格式如下：

```
import static package.ClassName.*;
```

上面语法中的星号只能代表静态成员变量或方法名。

import static 语句也放在 [Java](http://c.biancheng.net/java/) 源文件的 package 语句（如果有的话）之后、类定义之前，即放在与普通 import 语句相同的位置，而且 import 语句和 import static 语句之间没有任何顺序要求。

所谓静态成员变量、静态方法其实就是前面介绍的类变量、类方法，它们都需要使用 static 修饰，而 static 在很多地方都被翻译为静态，因此 import static 也就被翻译成了 “静态导入”。其实完全可以抛开这个翻译，用一句话来归纳 import 和 import static 的作用，使用 import 可以省略写包名，而使用 import static 可以省略类名。

下面程序使用 import static 语句来导入 java.lang.System 类下的全部静态成员变量，从而可以将程序简化成如下形式。

```
import static java.lang.System.*;import static java.lang.Math.*;public class StaticImportTest {    public static void main(String[] args) {        // out是java.lang.System类的静态成员变量，代表标准输出        // PI是java.lang.Math类的静态成员变量，表示π常量        out.println(PI);        // 直接调用Math类的sqrt静态方法，返回256的正平方根        out.println(sqrt(256));    }}
```

从上面程序不难看出，import 和 import static 的功能非常相似，只是它们导入的对象不一样而已。import 语句和 import static 语句都是用于减少程序中代码编写量的。

# static关键字（静态变量和静态方法）

在类中，使用 static 修饰符修饰的属性（成员变量）称为静态变量，也可以称为类变量，常量称为静态常量，方法称为静态方法或类方法，它们统称为静态成员，归整个类所有。

静态成员不依赖于类的特定实例，被类的所有实例共享，就是说 static 修饰的方法或者变量不需要依赖于对象来进行访问，只要这个类被加载，[Java](http://c.biancheng.net/java/) 虚拟机就可以根据类名找到它们。

调用静态成员的语法形式如下：

```
类名.静态成员
```

注意：

- static 修饰的成员变量和方法，从属于类。
- 普通变量和方法从属于对象。
- 静态方法不能调用非静态成员，编译会报错。

## 静态变量

类的成员变量可以分为以下两种：

1. 静态变量（或称为类变量），指被 static 修饰的成员变量。
2. 实例变量，指没有被 static 修饰的成员变量。


静态变量与实例变量的区别如下：

1）静态变量

- 运行时，Java 虚拟机只为静态变量分配一次内存，在加载类的过程中完成静态变量的内存分配。
- 在类的内部，可以在任何方法内直接访问静态变量。
- 在其他类中，可以通过类名访问该类中的静态变量。


2）实例变量

- 每创建一个实例，Java 虚拟机就会为实例变量分配一次内存。
- 在类的内部，可以在非静态方法中直接访问实例变量。
- 在本类的静态方法或其他类中则需要通过类的实例对象进行访问。


静态变量在类中的作用如下：

- 静态变量可以被类的所有实例共享，因此静态变量可以作为实例之间的共享数据，增加实例之间的交互性。
- 如果类的所有实例都包含一个相同的常量属性，则可以把这个属性定义为静态常量类型，从而节省内存空间。例如，在类中定义一个静态常量 PI。

```
public static double PI = 3.14159256;
```

#### 例 1

创建一个带静态变量的类，然后在 main() 方法中访问该变量并输出结果。

```
public class StaticVar {    public static String str1 = "Hello";    public static void main(String[] args) {        String str2 = "World!";        // 直接访问str1        String accessVar1 = str1+str2;        System.out.println("第 1 次访问静态变量，结果为："+accessVar1);        // 通过类名访问str1        String accessVar2 = StaticVar.str1+str2;        System.out.println("第 2 次访问静态变量，结果为："+accessVar2);        // 通过对象svt1访问str1        StaticVar svt1 = new StaticVar();        svt1.str1 = svt1.str1+str2;        String accessVar3 = svt1.str1;        System.out.println("第3次访向静态变量，结果为："+accessVar3);        // 通过对象svt2访问str1        StaticVar svt2 = new StaticVar();        String accessVar4 = svt2.str1+str2;        System.out.println("第 4 次访问静态变量，结果为："+accessVar4);    }}
```

运行该程序后的结果如下所示。

```
第 1 次访问静态变量，结果为：HelloWorld!
第 2 次访问静态变量，结果为：HelloWorld!
第 3 次访向静态变量，结果为：HelloWorld!
第 4 次访问静态变量，结果为：HelloWorld!World!
```

从运行结果可以看出，在类中定义静态的属性（成员变量），在 main() 方法中可以直接访问，也可以通过类名访问，还可以通过类的实例对象来访问。

注意：静态变量是被多个实例所共享的。

## 静态方法

与成员变量类似，成员方法也可以分为以下两种：

1. 静态方法（或称为类方法），指被 static 修饰的成员方法。
2. 实例方法，指没有被 static 修饰的成员方法。


静态方法与实例方法的区别如下：

- 静态方法不需要通过它所属的类的任何实例就可以被调用，因此在静态方法中不能使用 this 关键字，也不能直接访问所属类的实例变量和实例方法，但是可以直接访问所属类的静态变量和静态方法。另外，和 this 关键字一样，super 关键字也与类的特定实例相关，所以在静态方法中也不能使用 super 关键字。
- 在实例方法中可以直接访问所属类的静态变量、静态方法、实例变量和实例方法。

#### 例 2

创建一个带静态变量的类，添加几个静态方法对静态变量的值进行修改，然后在 main( ) 方法中调用静态方法并输出结果。

```
public class StaticMethod {    public static int count = 1;    // 定义静态变量count    public int method1() {            // 实例方法method1        count++;    // 访问静态变量count并赋值        System.out.println("在静态方法 method1()中的 count="+count);    // 打印count        return count;    }    public static int method2() {            // 静态方法method2        count += count;    // 访问静态变量count并赋值        System.out.println("在静态方法 method2()中的 count="+count);    // 打印count        return count;    }    public static void PrintCount() {            // 静态方法PrintCount        count += 2;        System.out.println("在静态方法 PrintCount()中的 count="+count);    // 打印count    }    public static void main(String[] args) {        StaticMethod sft = new StaticMethod();        // 通过实例对象调用实例方法        System.out.println("method1() 方法返回值 intro1="+sft.method1());        // 直接调用静态方法        System.out.println("method2() 方法返回值 intro1="+method2());        // 通过类名调用静态方法，打印 count        StaticMethod.PrintCount();    }}
```

运行该程序后的结果如下所示。

```
在静态方法 method1()中的 count=2
method1() 方法返回值 intro1=2
在静态方法 method2()中的 count=4
method2() 方法返回值 intro1=4
在静态方法 PrintCount()中的 count=6
```

在该程序中，静态变量 count 作为实例之间的共享数据，因此在不同的方法中调用 count，值是不一样的。从该程序中可以看出，在静态方法 method1() 和 PrintCount() 中是不可以调用非静态方法 method1() 的，而在 method1() 方法中可以调用静态方法 method2() 和 PrintCount()。

在访问非静态方法时，需要通过实例对象来访问，而在访问静态方法时，可以直接访问，也可以通过类名来访问，还可以通过实例化对象来访问。

## 静态代码块

静态代码块指 Java 类中的 static{ } 代码块，主要用于初始化类，为类的静态变量赋初始值，提升程序性能。

静态代码块的特点如下：

- 静态代码块类似于一个方法，但它不可以存在于任何方法体中。
- 静态代码块可以置于类中的任何地方，类中可以有多个静态初始化块。 
- Java 虚拟机在加载类时执行静态代码块，所以很多时候会将一些只需要进行一次的初始化操作都放在 static 代码块中进行。
- 如果类中包含多个静态代码块，则 Java 虚拟机将按它们在类中出现的顺序依次执行它们，每个静态代码块只会被执行一次。
- 静态代码块与静态方法一样，不能直接访问类的实例变量和实例方法，而需要通过类的实例对象来访问。

#### 例 3

编写一个 Java 类，在类中定义一个静态变量，然后使用静态代码块修改静态变量的值。最后在 main() 方法中进行测试和输出。

```
public class StaticCode {    public static int count = 0;    {        count++;        System.out.println("非静态代码块 count=" + count);    }    static {        count++;        System.out.println("静态代码块1 count=" + count);    }    static {        count++;        System.out.println("静态代码块2 count=" + count);    }    public static void main(String[] args) {        System.out.println("*************** StaticCode1 执行 ***************");        StaticCode sct1 = new StaticCode();        System.out.println("*************** StaticCode2 执行 ***************");        StaticCode sct2 = new StaticCode();    }}
```

如上述示例，为了说明静态代码块只被执行一次，特地添加了非静态代码块作为对比，并在主方法中创建了两个类的实例对象。上述示例的执行结果为：

```
静态代码块1 count=1
静态代码块2 count=2
*************** StaticCode1 执行 ***************
非静态代码块 count=3
*************** StaticCode2 执行 ***************
非静态代码块 count=4
```

上述代码中 { } 代码块为非静态代码块，非静态代码块是在创建对象时自动执行的代码，不创建对象不执行该类的非静态代码块。代码域中定义的变量都是局部的，只有域中的代码可以调用。 