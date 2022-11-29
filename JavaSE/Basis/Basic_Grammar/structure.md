# 编写Java源程序

1. 新建文件并将文件名后缀改为小写的`.java`

   ![image-20220821210512676](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208221912740.png)

2. 通过记事本打开文件，输入并保存：

   ```java
    public class HelloWorld{    //类名    
        public static void main(String[] args){ //mian方法        
            System.out.println("Hello world!"); //输出    
        }
    }
   ```

**提示**：保存的文件名中不能出现空格，类似"`Hello Java.java`"的文件名在编译时会出现找不到文件的错误。

**注意**：

- 一个程序的基本单位就是`class`表示类，HelloWorld是类名，**类名要与代码文件名一致**，大括号内是类的内容。一个类可以有多个方法(详细请查看 [类](../Reference_Types/Class/README.md)的使用)

- `public static void main(String[] args)`：main方法的定义。程序最开始执行的地方。

  main方法是Java程序的入口，一个程序只能有一个main方法。

- [`System.out.println`](in_out.md#print向屏幕输出)是Java提供的内置功能，可以将双引号的内容输出，在没有参数的情况下， [`System.out.println()`](in_out.md#print向屏幕输出)会输出一行空行

- 在方法内部，语句才是真正的执行代码。**Java的每一行语句必须以分号结束**。

- 关键字 [`public`](../../Advanced/Object_Oriented/Keyword/Access_Modifier/README.md) 表示访问说明符，表明该类是一个公共类，可以控制其他对象对类成员的访问。

- 关键字 [`static`](../../Advanced/Object_Oriented/Keyword/Access_Modifier/static.md) 表示该方法是一个静态方法，允许调用 main() 方法，无须创建类的实例。

- 关键字 [`void`](../../Advanced/Object_Oriented/Keyword/Access_Modifier/void.md) 表示 main() 方法没有返回值。

- "`/*`" "`*/`"之间的内容和以"`//`"开始的内容为 Java 程序的[注释](comment.md)。

# 运行Java程序

Java源码本质上是一个文本文件，我们需要先用`javac`把`Hello.java`编译成字节码文件`Hello.class`，然后，用`java`命令执行这个字节码文件：

![Java运行过程](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208212140741.png)

**说明**：可执行文件`javac`是编译器，而可执行文件`java`就是虚拟机。
第一步，在保存`Hello.java`的目录下执行命令`javac Hello.java`：

```shell
$ javac Hello.java
```

如果源代码无误，上述命令不会有任何输出，而当前目录下会产生一个`Hello.class`文件：

```shell
$ ls
Hello.class	Hello.java
```

第二步，执行`Hello.class`，使用命令`java Hello`：

```shell
$ java Hello
Hello, world!
```

**注意**：给虚拟机传递的参数Hello是我们定义的类名，虚拟机自动查找对应的class文件并执行。
直接运行`java Hello.java`也是可以的：

```shell
$ java Hello.java
Hello, world!
```

这是Java 11新增的一个功能，它可以直接运行一个单文件源码！
需要注意的是，在实际项目中，单个不依赖第三方库的Java源码是非常罕见的，所以，绝大多数情况下，我们无法直接运行一个Java源码文件，原因是它需要依赖其他的库

# 编译常见错误解决方法

在使用 javac 编译器编译源代码文件时，可能会出现下面几个常见问题：

1. `Error:cannot read:HelloJava.java javac`

   工具程序找不到指定的 java 文件，需要检查文件是否存储在当前目录中，或文件名是否错误。

2. `HelloJava.java:4:class HelloJava is public,should be declared in a file named MyApplication.java`

   源文件中类的名称和源文件名称不符，需要确定源文件名称和类名称是否相同。

3. `HelloJava.java:6:cannot find symbol`

   源程序文件中某些代码部分输入错了，最常产生的原因可能是没有注意到字母的大小写。

Javac 不是内部或外部命令、可执行程序或批量文件。path 设置有误或没有在 path 系统变量中加入 JDK 的 bin 目录。

如果没有出现上述所列问题，即成功编译了该 Java 文件。在解释执行 .class 文件时，可能会出现下面几个常见问题。

1. `Exception in thread “main” java.lang.NoClassDe£FoundError`

   Java 工具程序找不到所指定的 .class 类，需要确定指定的类是否存储在当前目录中，名称是否正确。

2. `Exception in thread “main” java.lang.NoSuchMetliodError:main`

   没有指定 Java 程序的入口。Java 工具程序指定的类必须有一个程序入口，也就是必须包括 `main(String args[])` 这个方法。

# 初次编程所牢记的知识点

## 大小写问题

**Java 是区分大小写的语言**。

如果编写的 Java 程序的类是 `HelloJava`，但当他运行 Java 程序时，运行的则是 `java hellojava` 这种形式，这种错误的形式没有严格按 Java 程序中编写的来写，可能引起系统提示如图 1 所示的错误。

![大小写问题错误](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208212144925.png)


因此这里必须提醒大家，在 Java 程序里，`HelloJava` 和 `hellojava` 是完全不同的，必须严格注意 Java 程序里的大小写问题。

必须严格注意 Java 程序中每个单词的大小写，不要随意编写。例如 `class` 和 `Class` 是不同的两个词，`class` 是正确的，但是如果写成 `Class`，则程序无法编译通过。

实际上，Java 程序中的关键字全部是小写的，无需大写任何字母。

## 路径里包含空格的问题

这是一个更容易引起错误的问题。由于 Windows 系统的很多路径都包含了空格，典型的例如 Program Files 文件夹，而且这个文件夹是 JDK 的默认安装路径。

如果 `CLASSPATH` 环境变量里包含的路径中存在空格，则可能引发错误。因此，推荐大家安装 JDK 以及 Java 相关程序、工具时，不要安装在包含空格的路径下，否则可能引发错误。

## `main` 方法的问题

如果需要用 java 命令直接运行一个 Java 类，这个 Java 类必须包含 main 方法，这个 main 方法必须使用 `public` 和 `static` 来修饰，必须使用 `void` 声明该方法的返回值，而且该方法的参数类型只能是一个字符串数组，而不能是其他形式的参数。对于这个 main 方法而言，前面的 `public` 和 `static` 修饰符的位置可以互换，但其他部分则是固定的。

定义 main 方法时，不要写成 Main 方法，如果不小心把方法名的首字母写成了大写，编译时不会出现任何问题，但运行该程序时将给出错误提示：

![错误提示](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208212146499.png)


这个错误提示找不到 main 方法，因为 Java 虚拟机只会选择从 main 方法开始执行。对于 Main 方法，Java 虚拟机会把该方法当成一个普通方法，而不是程序的入口。

main 方法里可以放置程序员需要执行的可执行性语句，例如 `System.out.println("Hello Java!")`，这行语句是 Java 里的输出语句，用于向控制台输岀“Hello Java!”这个字符串内容，输出结束后还输出一个换行符。

