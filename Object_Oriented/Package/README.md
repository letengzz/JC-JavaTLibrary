# 包

## 创建包

### 使用IDEA

![image-20221023223335814](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232233356.png)

**注意**：也可以定义Class时，写入 `包名.类名`即可完成创建包及创建类。

### 使用Eclipse

略

## 定义包(package)

在编写 Java 程序时，随着程序架构越来越大，类的个数也越来越多，这时就会发现管理程序中维护类名称也是一件很麻烦的事，尤其是一些同名问题的发生。有时，开发人员还可能需要将处理同一方面的问题的类放在同一个目录下，以便于管理。

为了解决上述问题，Java 引入了包(package)机制，提供了类的多层命名空间，**用于解决类的命名冲突、类文件管理等问题**。

包允许将类组合成较小的单元（类似文件夹），它基本上隐藏了类，并避免了名称上的冲突。包允许在更广泛的范围内保护类、数据和方法。你可以在包内定义类，而在包外的代码不能访问该类。这使你的类相互之间有隐私，但不被其他世界所知。

包的**作用**：

1. 区分相同名称的类，解决名字冲突问题。
2. 对包进行分类管理，能够较好地管理大量的类。
3. 控制访问范围。

Java 中使用 package 语句定义包，**package 语句应该放在源文件的第一行，在每个源文件中只能有一个包定义语句，并且 package 语句适用于所有类型**(类、接口、枚举和注释)的文件。

**语法格式**：

```java
package 包名;
```

Java 包的**命名规则**：

- 包名全部由小写字母（多个单词也全部小写）。
- 如果包名包含多个层次，每个层次用"`.`"分割。
- 为了避免名字冲突，我们需要确定唯一的包名。推荐的做法是使用倒置的域名来确保唯一性。包名一般由倒置的域名开头，比如 `com.baidu`，不要有 www。
- 子包就可以根据功能自行命名。


**注意**：不要和`java.lang`包的类重名，即自己的类不要使用这些名字：String、System、Runtime、...  也不要和JDK常用类重名：`java.util.List`、`java.text.Format`、`java.math.BigInteger`、...

- 自定义包不能 java 开头。

**注意**：如果在源文件中没有定义包，那么类、接口、枚举和注释类型文件将会被放进一个无名的包中，也称为默认包。在实际企业开发中，通常不会把类定义在默认包下。

## 导入包(import)

如果使用不同包中的其它类，需要使用该类的全名（包名+类名）。代码如下：

```java
example.Test test = new example.Test();
```

- example 是包名
- Test 是包中的类名
- test 是类的对象。

为了简化编程，Java 引入了 import 关键字，import 可以向某个 Java 文件中导入指定包层次下的某个类或全部类。**import 语句位于 package 语句之后，类定义之前**。一个 Java 源文件只能包含一个 package 语句，但**可以包含多个 import 语句**。

### 导入单个类的语法

用于直接导入指定类。

**语法格式**：

```java
import 包名.类名;
```

**例**：导入前面的 example.Test 类：

```
import example.Test;
```

### 导入指定包下全部类

**语法格式**：

```java 
import example.*;
```

 import 语句中的星号(`*`)只能代表类，不能代表包，表明导入 example 包下的所有类。

**提示**：使用星号(`*`)可能会增加编译时间，特别是引入多个大包时，所以明确的导入你想要用到的类是一个好方法，需要注意的是使用星号对运行时间和类的大小没有影响。

### 静态导入

在 JDK 1.5 之后增加了一种静态导入的语法，**用于导入指定类的某个静态成员变量、方法或全部的静态成员变量、方法**。如果一个类中的方法全部是使用 static 声明的静态方法，则在导入时就可以直接使用 import static 的方式导入。

import 和 import static 的功能非常相似，只是它们导入的对象不一样而已。import 语句和 import static 语句都是用于减少程序中代码编写量的。

#### 导入指定类的单个静态成员变量

**语法格式**：

```java
import static package.ClassName.fieldName|methodName;
```

上面语法导入 package.ClassName 类中名为 fieldName 的静态成员变量或者名为 methodName 的静态方法。例如，可以使用`import static java.lang.System.out;`语句来导入 java.lang.System 类的 out 静态成员变量。

#### 导入指定类的方法和全部静态成员变量、方法

**语法格式**：

```java
import static package.ClassName.*;
```

- 星号只能代表静态成员变量或方法名。


import static 语句也放在 Java 源文件的 package 语句(如果有的话)之后、类定义之前，即放在与普通 import 语句相同的位置，而且 import 语句和 import static 语句之间没有任何顺序要求。

 **import 和 import static 的作用**：使用 import 可以省略写包名，而使用 import static 可以省略类名。

**例**：

使用 import static 语句来导入 java.lang.System 类下的全部静态成员变量：

```java
import static java.lang.System.*;
import static java.lang.Math.*;
public class StaticImportTest {    
    public static void main(String[] args) {        
        // out是java.lang.System类的静态成员变量，代表标准输出        
        // PI是java.lang.Math类的静态成员变量，表示π常量        
        out.println(PI);        
        // 直接调用Math类的sqrt静态方法，返回256的正平方根        
        out.println(sqrt(256));    
    }
}
```

#### 导入一个类的静态字段和静态方法

```java
package main;

// 导入System类的所有静态字段和静态方法:
import static java.lang.System.*;

public class Main {
    public static void main(String[] args) {
        // 相当于调用System.out.println(…)
        out.println("Hello, world!");
    }
}
```

#### 注意

- `import static`很少使用。

### 注意

通过使用 import 语句可以简化编程，但 import 语句并不是必需的，如果在类里使用其它类的全名，可以不使用 import 语句。

Java 默认为所有源文件导入 java.lang 包下的所有类，因此前面在 Java 程序中使用 String、System 类时都无须使用 import 语句来导入这些类。但数组时提到的 Arrays 类，其位于 java.util 包下，则必须使用 import 语句来导入该类。

在一些极端的情况下，import 语句也帮不了我们，此时只能在源文件中使用类全名。例如，需要在程序中使用 java.sql 包下的类，也需要使用 java.util 包下的类，则可以使用如下两行 import 语句：

```java
import java.util.*;
import java.sql.*;
```

如果接下来在程序中需要使用 Date 类，则会引起如下编译错误：

> Test.java:25:对Date的引用不明确，
> java.sql中的类java.sql.Date和java.util中的类java.util.Date都匹配

错误提示：在 Test.java 文件的第 25 行使用了 Date 类，而 import 语句导入的 `java.sql` 和 `java.util` 包下都包含了 Date 类，系统不知道使用哪个包下的 Date 类。在这种情况下，如果需要指定包下的 Date 类，则只能使用该类的全名：

```java
// 为了让引用更加明确，即使使用了 import 语句，也还是需要使用类的全名
java.sql.Date d = new java.sql.Date();
```

------

Java编译器最终编译出的`.class`文件只使用完整类名，因此，在代码中，当编译器遇到一个`class`名称时：

- 如果是完整类名，就直接根据完整类名查找这个`class`；
- 如果是简单类名，按下面的顺序依次查找：
  - 查找当前`package`是否存在这个`class`；
  - 查找`import`的包是否包含这个`class`；
  - 查找`java.lang`包是否包含这个`class`。

如果按照上面的规则还无法确定类名，则编译报错。

**例**：

```java
// Main.java
package test;

import java.text.Format;

public class Main {
    public static void main(String[] args) {
        java.util.List list; // ok，使用完整类名 -> java.util.List
        Format format = null; // ok，使用import的类 -> java.text.Format
        String s = "hi"; // ok，使用java.lang包的String -> java.lang.String
        System.out.println(s); // ok，使用java.lang包的System -> java.lang.System
        MessageFormat mf = null; // 编译错误：无法找到MessageFormat: MessageFormat cannot be resolved to a type
    }
}
```

因此，编写class的时候，编译器会自动帮我们做两个import动作：

- 默认自动`import`当前`package`的其他`class`；
- 默认自动`import java.lang.*`。

**注意**：

- 自动导入的是java.lang包，但类似java.lang.reflect这些包仍需要手动导入。

- 如果有两个`class`名称相同，例如，`mr.jun.Arrays`和`java.util.Arrays`，那么只能`import`其中一个，另一个必须写完整类名。

------

在Java虚拟机执行的时候，JVM只看完整类名，因此，只要包名不同，类就不同。

包可以是多层结构，用`.`隔开。例如：`java.util`。

**注意**：包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。

没有定义包名的`class`，它使用的是默认包，非常容易引起名字冲突，因此，不推荐不写包名的做法。

我们还需要按照包结构把上面的Java文件组织起来。假设以`package_sample`作为根目录，`src`作为源码目录，那么所有文件结构就是：

![image-20221023222658155](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232232164.png)

即所有Java文件对应的目录层次要和包的层次一致。

编译后的`.class`文件也需要按照包结构存放。如果使用IDE，把编译后的`.class`文件放到`bin`目录下，那么，编译的文件结构就是：

![image-20221023222714525](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232232413.png)

编译的命令相对比较复杂，我们需要在`src`目录下执行`javac`命令：

```java
javac -d ../bin ming/Person.java hong/Person.java mr/jun/Arrays.java
```

在IDE中，会自动根据包结构编译所有Java源码，所以不必担心使用命令行编译的复杂命令。

## 系统包

Java SE 提供了一些系统包，其中包含了 Java 开发中常用的基础类。在 Java 语言中，开发人员可以自定义包，也可以使用系统包，常用的系统包：

![](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232203041.png)

## 包作用域

位于同一个包的类，可以访问包作用域的字段和方法。不用`public`、`protected`、`private`修饰的字段和方法就是包作用域。

**例**：`Person`类定义在`hello`包下面

```
package hello;

public class Person {
    // 包作用域:
    void hello() {
        System.out.println("Hello!");
    }
}
```

`Main`类也定义在`hello`包下面：

```
package hello;

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.hello(); // 可以调用，因为Main和Person在同一个包
    }
}
```

# 使用自定义包

1. 创建一个名为 com.dao 的包。

2. 向 com.dao 包中添加一个 Student 类，该类包含一个返回 String 类型数组的 GetAll() 方法。Student 类代码如下：

   ```java
   package com.dao;public class Student {    
       public static String[] GetAll() {        
           String[] namelist = {"李潘","邓国良","任玲玲","许月月","欧阳娜","赵晓慧"};   
           return namelist;    
       }
   }
   ```

3. 创建 com.test 包，在该包里创建带 main() 方法的 Test 类。

4. 在 main() 方法中遍历 Student 类的 GetAll() 方法中的元素内容，在遍历内容之前，使用 import 引入 com.dao 整个包：

   ```java
   package com.test;
   import com.dao.Student;
   public class Test {    
       public static void main(String[] args) {        
           System.out.println("学生信息如下：");        
           for(String str:Student.GetAll()) {
               System.out.println(str);        
           }    
       }
   }
   ```

5. 输出结果：

   > 学生信息如下：
   > 李潘
   > 邓国良
   > 任玲玲
   > 许月月
   > 欧阳娜
   > 赵晓慧

# 使用CMD来操作

先定义包后使用

```shell
javac -d . Demo.java
```

执行就要写 全称定路径名

```java
java 类名.文件名
```

# 总结

- Java内建的`package`机制是为了避免`class`命名冲突


- JDK的核心类使用`java.lang`包，编译器会自动导入


- JDK的其它常用类定义在`java.util.*`，`java.math.*`，`java.text.*`，……


- 包名推荐使用倒置的域名，例如`org.apache`