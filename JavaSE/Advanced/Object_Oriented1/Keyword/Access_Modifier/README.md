# 访问修饰符

在Java中，用[public]()、[protected]()、[private]()、[缺省]()来限定访问作用域。

**信息隐藏**是 OOP 最重要的功能之一，也是使用访问修饰符的原因。在编写程序时，有些核心数据往往不希望被用户调用，需要控制这些数据的访问。

对类成员访问的限制是面向对象程序设计的一个基础，这有利于防止对象的误用。只允许通过一系列定义完善的方法来访问私有数据，就可以（通过执行范围检查）防止数据赋予不正当的值。例如，类以外的代码不可能直接向一个私有成员赋值。同时，还可以精确地控制如何以及何时使用对象中的数据。

当正确实现对类成员的方法控制后，类就可以创建一个可用的“黑箱”，其内部动作不会被打开而任意篡改。

通过使用访问控制修饰符来限制对对象私有属性的访问，可以获得 3 个重要的好处。

- 防止对封装数据的未授权访问。
- 有助于保证数据完整性。
- 当类的私有实现细节必须改变时，可以限制发生在整个应用程序中的“连锁反应”。

------

访问控制符是一组限定类、属性或方法是否可以被程序里的其他部分访问和调用的修饰符。类的访问控制符只能是空或者 public，方法和属性的访问控制符有 4 个，分别是 public、 private、protected 和 friendly，其中 friendly 是一种没有定义专门的访问控制符的默认情况。

访问控制在面向对象技术中处于很重要的地位，合理地使用访问控制符，可以通过降低类和类之间的耦合性（关联性）来降低整个项目的复杂度，也便于整个项目的开发和维护。在 Java 语言中，访问控制修饰符有 4 种。



![](D:/Data/typora/photo/%E5%9B%BE%E7%89%8733-16665890630752.png)

- [public]()
- [default]()
- [private]()
- [protected]()

如果不确定是否需要`public`，就不声明为`public`，即尽可能少地暴露对外的字段和方法。

把方法定义为`package`权限有助于测试，因为测试类和被测试类只要位于同一个`package`，测试代码就可以访问被测试类的`package`权限方法。

一个`.java`文件只能包含一个`public`类，但可以包含多个非`public`类。如果有`public`类，文件名必须和`public`类的名字相同。

### 小结

Java内建的访问权限包括`public`、`protected`、`private`和`package`权限；

Java在方法内部定义的变量是局部变量，局部变量的作用域从变量声明开始，到一个块结束；

`final`修饰符不是访问权限，它可以修饰`class`、`field`和`method`；

一个`.java`文件只能包含一个`public`类，但可以包含多个非`public`类。




#### 

**例**：

1. 新建 Student.java 文件，在该文件中定义不同修饰符的属性和方法，代码如下：

```
class Student {    // 姓名，其访问权限为默认(friendly)    String name;    // 定义私有变量，身份证号码    private String idNumber;    // 定义受保护变量，学号    protected String no;    // 定义共有变量，邮箱    public String email;    // 定义共有方法，显示学生信息    public String info() {        return"姓名："+name+"，身份证号码："+idNumber+"，学号："+no+"，邮箱："+email;    }}
```

2. 新建 StudentTest.java 文件，在该文件中定义 main() 方法，访问 Student 类中的属性并赋值，打印出用户的信息。代码如下：

```
public class StudentTest {    public static void main(String[] args) {        // 创建Student类对象        Student stu = new Student();        // 向Student类对象中的属性赋值        stu.name = "zhht";        // stu.idNumber="043765290763137806";        // 这是不允许的。提示stu.idNumber是不可见的，必须注释掉才可运行        stu.no = "20lil01637";        stu.email = "zhht@qq.com";        System.out.println(stu.info());    }}
```

在 StudentTest 类中，“stu.idNumber="043765290763137806";”代码行将提示 “The field User.password is not visible”错误信息。将该代码行注释掉再运行 StudentTest.java 文件，输出的内容如下：

```
姓名：zhht，身份证号码：null，学号：20lil01637，邮箱：zhht@qq.com
```


在源文件中创建了两个类，分别为主类 StudentTest 和辅助类 Student，二者在同一个包中。

在辅助类 Student 中，创建了 4 个属性，其访问控制分别为默认的、私有的、受保护的和共有的，除了私有控制符修饰的变量之外，其他的都可以被主类访问，同时创建了一个共有的方法——info()，用于打印用户信息。

在主类 StudentTest 中，创建类 Student 的实例化对象 stu，通过对象 stu 来访问该对象中的属性并赋值，因为 idNumber 属性的修饰符为 private（私有的），因此，在 StudentTest 类中的 main() 方法中无法访问该属性。

从上面的例子中可以看出，范围控制修饰符成功地限制了访问者访问不同修饰符的属性（成员变量），从而实现了数据的隐藏。