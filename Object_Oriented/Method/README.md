# method方法

在`class`内部，可以定义若干方法（`method`）：

```java
public class Hello {
    public static void main(String[] args) { // 方法名是main
        // 方法代码...
    } // 方法定义结束
}
```

方法定义了一组执行语句，方法内部的代码将会被依次顺序执行。

这里的方法名是`main`，返回值是`void`，表示没有任何返回值。

**注意**：`public`除了可以修饰`class`外，也可以修饰方法。而关键字`static`是另一个修饰符，它表示静态方法，Java入口程序规定的方法必须是静态方法，方法名必须为`main`，括号内的参数必须是String数组。

## 方法名要求

**注意**：

- 类名必须以英文字母开头，后接字母，数字和下划线的组合。

- 以小写字母开头。

- 好的方法命名：

  - main

  - goodMorning

  - playVR

- 不好的方法命名：

  - Main

  - good123

  - good_morning

  - _playVR

## 定义`Method`

**基本语法**：

```java
修饰符 方法返回类型 方法名(方法参数列表) {
    若干方法语句;
    return 方法返回值;
}
```

方法返回值通过`return`语句实现，如果没有返回值，返回类型设置为`void`，可以省略`return`。

一个`class`可以包含多个`field`(Java中也可以叫`Method`方法)

```java
class Person {
    public String name;	//定义name方法(字段)
    public int age;	//定义age方法(字段)
}
```

## 方法参数

方法可以包含0个或任意个参数。方法参数用于接收传递给方法的变量值。

调用方法时，必须严格按照参数的定义一一传递。

```java
class Person {
    ...
    public void setNameAndAge(String name, int age) {
        ...
    }
}
```

调用这个`setNameAndAge()`方法时，必须有两个参数，且第一个参数必须为`String`，第二个参数必须为`int`：

```java
public class Main(){
    public static void main(String[] args){
        Person ming = new Person();
		ming.setNameAndAge("Xiao Ming"); // 编译错误：参数个数不对
		ming.setNameAndAge(12, "Xiao Ming"); // 编译错误：参数类型不对
        ming.setNameAndAge("Xiao Ming",12); // 编译错误：参数类型不对
    }
}
```

## 可变参数

可变参数用`类型...`定义，可变参数相当于数组类型：

```java 
class Group {
    private String[] names;

    public void setNames(String... names) {
        this.names = names;
    }
}
```

上面的`setNames()`就定义了一个可变参数。调用时，可以自己选择参数长度：

```java
public class Main(){
    public static void main(String[] args){
        Group g = new Group();
		g.setNames("Xiao Ming", "Xiao Hong", "Xiao Jun"); // 传入3个String
		g.setNames("Xiao Ming", "Xiao Hong"); // 传入2个String
		g.setNames("Xiao Ming"); // 传入1个String
		g.setNames(); // 传入0个String
    }
}
```

完全可以把可变参数改写为`String[]`类型：

```
class Group {
    private String[] names;

    public void setNames(String[] names) {
        this.names = names;
    }
}
```

但是，调用方需要自己先构造`String[]`，比较麻烦。

```java 
public class Main(){
    public static void main(String[] args){
		Group g = new Group();
		g.setNames(new String[] {"Xiao Ming", "Xiao Hong", "Xiao Jun"}); // 传入1个String[]
    }
}
```

调用方可以传入`null`：

```java 
public class Main(){
    public static void main(String[] args){
		Group g = new Group();
		g.setNames(null);
    }
}
```

**注意**：可变参数可以保证无法传入`null`，因为传入0个参数时，接收到的实际值是一个空数组而不是`null`。



在具体实际开发过程中，有时方法中参数的个数是不确定的。为了解决这个问题，在 J2SE 5.0 版本中引入了可变参数的概念。

声明可变参数的语法格式如下：

```
methodName({paramList},paramType…paramName)
```

其中，methodName 表示方法名称；paramList 表示方法的固定参数列表；paramType 表示可变参数的类型；… 是声明可变参数的标识；paramName 表示可变参数名称。

注意：可变参数必须定义在参数列表的最后。

#### 例 1

每次参加考试的人数是不固定的，但是每次考试完之后都需要打印出本次考试的总人数以及参加考试的学生名单。下面编写程序，使用方法的可变参数实现该功能，具体的代码如下：

```
public class StudentTestMethod {    // 定义输出考试学生的人数及姓名的方法    public void print(String...names) {        int count = names.length;    // 获取总个数        System.out.println("本次参加考试的有"+count+"人，名单如下：");        for(int i = 0;i < names.length;i++) {            System.out.println(names[i]);        }    }    public static void main(String[] args) {        // TODO Auto-generated method stub        StudentTestMethod student = new StudentTestMethod();        student.print("张强","李成","王勇");    // 传入3个值        student.print("马丽","陈玲");    }}
```

在 Student TestMethod 类中定义了 print() 方法和 main() 方法。print() 方法声明了一个 String 类型的可变参数，方法体打印可变参数的总个数以及参数值。在 main() 方法中创建了 StudentTestMethod 类的实例，然后分别传入不同个数的参数调用 print() 方法。

运行 StudentTestMethod 类，输出结果如下：

```
本次参加考试的有3人，名单如下：
张强
李成
王勇
本次参加考试的有2人，名单如下：
马丽
陈玲
```

## 参数绑定

调用方把参数传递给实例方法时，调用时传递的值会按参数位置一一绑定。

**基本类型参数的传递**：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        int n = 15; // n的值为15
        p.setAge(n); // 传入n的值
        System.out.println(p.getAge()); // 15
        n = 20; // n的值改为20
        System.out.println(p.getAge()); // 15
    }
}

class Person {
    private int age;

    public int getAge() {
        return this.age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

​	运行代码，从结果可知，修改外部的局部变量`n`，不影响实例`p`的`age`字段，原因是`setAge()`方法获得的参数，复制了`n`的值，因此，`p.age`和局部变量`n`互不影响。

**引用类型参数的传递**：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        String[] fullname = new String[] { "Homer", "Simpson" };
        p.setName(fullname); // 传入fullname数组
        System.out.println(p.getName()); // "Homer Simpson"
        fullname[0] = "Bart"; // fullname数组的第一个元素修改为"Bart"
        System.out.println(p.getName()); //"Bart Simpson"
    }
}

class Person {
    private String[] name;

    public String getName() {
        return this.name[0] + " " + this.name[1];
    }

    public void setName(String[] name) {
        this.name = name;
    }
}
```

​	注意到`setName()`的参数现在是一个数组。一开始，把`fullname`数组传进去，然后，修改`fullname`数组的内容，结果发现，实例`p`的字段`p.name`也被修改了！

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        String bob = "Bob";
        p.setName(bob); // 传入bob变量
        System.out.println(p.getName()); // "Bob"
        bob = "Alice"; // bob改名为Alice
        System.out.println(p.getName()); // "Bob"
    }
}

class Person {
    private String name;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

**结论**：

- 基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响。

- 引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象。双方任意一方对这个对象的修改，都会影响对方。