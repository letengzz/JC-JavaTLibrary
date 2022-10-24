# 继承性

程序中的继承性是指子类拥有父类的全部特征和行为，这是类之间的一种关系。

**注意**：**Java 只支持单继承**。

**例**：

定义一个语文老师类和数学老师类，如果不采用继承方式，那么两个类中需要定义的属性和方法：

![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210181133408.jpeg)


语文老师类和数学老师类中的许多属性和方法相同，这些相同的属性和方法可以提取出来放在一个父类中，这个父类用于被语文老师类和数学老师类继承。当然父类还可以继承别的类：

![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210181133982.jpeg)

可以概括为：

![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210181135113.jpg)

学校主要人员是一个大的类别，老师和学生是学校主要人员的两个子类，而老师又可以分为语文老师和数学老师两个子类，学生也可以分为班长和组长两个子类。

使用这种层次形的分类方式，是为了将多个类的通用属性和方法提取出来，放在它们的父类中，然后只需要在子类中各自定义自己独有的属性和方法，并以继承的形式在父类中获取它们的通用属性和方法即可。

**提示**：C++ 支持多继承，多继承就是一个子类可有多个父类。例如，客轮是轮船也是交通工具，客轮的父类是轮船和交通工具。多继承会引起很多冲突问题，因此现在很多面向对象的语言都不支持多继承。Java 语言是单继承的，即只能有一个父类，但 Java 可以实现多个接口（接口类似于类，但接口的成员没有执行体），可以防止多继承所引起的冲突问题。
