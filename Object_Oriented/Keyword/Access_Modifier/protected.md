## protected关键字

`protected`允许子类访问父类的字段和方法。

继承有个特点，就是子类无法访问父类的`private`字段或者`private`方法。例如，`Student`类就无法访问`Person`类的`name`和`age`字段：

```
class Person {
    private String name;
    private int age;
}

class Student extends Person {
    public String hello() {
        return "Hello, " + name; // 编译错误：无法访问name字段
    }
}
```

这使得继承的作用被削弱了。为了让子类可以访问父类的字段，我们需要把`private`改为`protected`。用`protected`修饰的字段可以被子类访问：

```
class Person {
    protected String name;
    protected int age;
}

class Student extends Person {
    public String hello() {
        return "Hello, " + name; // OK!
    }
}
```

因此，`protected`关键字可以把字段和方法的访问权限控制在继承树内部，一个`protected`字段和方法可以被其子类，以及子类的子类所访问，后面我们还会详细讲解。

#### protected

用保护访问控制符 protected 修饰的类成员可以被三种类所访问：该类自身、与它在同一个包中的其他类以及在其他包中的该类的子类。使用 protected 修饰符的主要作用，是允许其他包中它的子类来访问父类的特定属性和方法，否则可以使用默认访问控制符。



### protected

`protected`作用于继承关系。定义为`protected`的字段和方法可以被子类访问，以及子类的子类：

```
package abc;

public class Hello {
    // protected方法:
    protected void hi() {
    }
}
```

上面的`protected`方法可以被继承的类访问：

```
package xyz;

class Main extends Hello {
    void foo() {
        // 可以访问protected方法:
        hi();
    }
}
```

### 