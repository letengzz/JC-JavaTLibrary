# final关键字

继承可以允许子类覆写父类的方法。如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为`final`。用`final`修饰的方法不能被`Override`：

```
class Person {
    protected String name;
    public final String hello() {
        return "Hello, " + name;
    }
}

Student extends Person {
    // compile error: 不允许覆写
    @Override
    public String hello() {
    }
}
```

如果一个类不希望任何其他类继承自它，那么可以把这个类本身标记为`final`。用`final`修饰的类不能被继承：

```
final class Person {
    protected String name;
}

// compile error: 不允许继承自Person
Student extends Person {
}
```

对于一个类的实例字段，同样可以用`final`修饰。用`final`修饰的字段在初始化后不能被修改。例如：

```
class Person {
    public final String name = "Unamed";
}
```

对`final`字段重新赋值会报错：

```
Person p = new Person();
p.name = "New Name"; // compile error!
```

可以在构造方法中初始化final字段：

```
class Person {
    public final String name;
    public Person(String name) {
        this.name = name;
    }
}
```

这种方法更为常用，因为可以保证实例一旦创建，其`final`字段就不可修改。

final 在 [Java](http://c.biancheng.net/java/) 中的意思是最终，也可以称为完结器，表示对象是最终形态的，不可改变的意思。final 应用于类、方法和变量时意义是不同的，但本质是一样的，都表示不可改变，类似 [C#](http://c.biancheng.net/csharp/) 里的 sealed 关键字。

使用 final 关键字声明类、变量和方法需要注意以下几点：

- final 用在变量的前面表示变量的值不可以改变，此时该变量可以被称为常量。
- final 用在方法的前面表示方法不可以被重写（子类中如果创建了一个与父类中相同名称、相同返回值类型、相同参数列表的方法，只是方法体中的实现不同，以实现不同于父类的功能，这种方式被称为方法重写，又称为方法覆盖。这里了解即可，教程后面我们会详细讲解）。
- final 用在类的前面表示该类不能有子类，即该类不可以被继承。

## final 修饰变量

final 修饰的变量即成为常量，只能赋值一次，但是 final 所修饰局部变量和成员变量有所不同。

1. final 修饰的局部变量必须使用之前被赋值一次才能使用。
2. final 修饰的成员变量在声明时没有赋值的叫“空白 final 变量”。空白 final 变量必须在构造方法或静态代码块中初始化。

注意：final 修饰的变量不能被赋值这种说法是错误的，严格的说法是，final 修饰的变量不可被改变，一旦获得了初始值，该 final 变量的值就不能被重新赋值。

```
public class FinalDemo {    void doSomething() {        // 没有在声明的同时赋值        final int e;        // 只能赋值一次        e = 100;        System.out.print(e);        // 声明的同时赋值        final int f = 200;    }    // 实例常量    final int a = 5; // 直接赋值    final int b; // 空白final变量    // 静态常量    final static int c = 12;// 直接赋值    final static int d; // 空白final变量    // 静态代码块    static {        // 初始化静态变量        d = 32;    }    // 构造方法    FinalDemo() {        // 初始化实例变量        b = 3;        // 第二次赋值，会发生编译错误        // b = 4;    }}
```

上述代码第 4 行和第 6 行是声明局部常量，其中第 4 行只是声明没有赋值，但必须在使用之前赋值（见代码第 6 行），其实局部常量最好在声明的同时初始化。代码第 13、14、16 和 17 行都声明成员常量。代码第 13 和 14 行是实例常量，如果是空白 final 变量（见代码第 14 行），则需要在构造方法中初始化（见代码第 27 行）。代码第 16 和 17 行是静态常量，如果是空白 final 变量（见代码第 17 行），则需要在静态代码块中初始化（见代码第 21 行）。

另外，无论是那种常量只能赋值一次，见代码第 29 行为 b 常量赋值，因为之前 b 已经赋值过一次，因此这里会发生编译错误。

#### final 修饰基本类型变量和引用类型变量的区别

当使用 final 修饰基本类型变量时，不能对基本类型变量重新赋值，因此基本类型变量不能被改变。 但对于引用类型变量而言，它保存的仅仅是一个引用，final 只保证这个引用类型变量所引用的地址不会改变，即一直引用同一个对象，但这个对象完全可以发生改变。

下面程序示范了 final 修饰数组和 Person 对象的情形。

```
import java.util.Arrays;class Person {    private int age;    public Person() {    }    // 有参数的构造器    public Person(int age) {        this.age = age;    }    // 省略age的setter和getter方法    // age 的 setter 和 getter 方法}public class FinalReferenceTest {    public static void main(String[] args) {        // final修饰数组变量，iArr是一个引用变量        final int[] iArr = { 5, 6, 12, 9 };        System.out.println(Arrays.toString(iArr));        // 对数组元素进行排序，合法        Arrays.sort(iArr);        System.out.println(Arrays.toString(iArr));        // 对数组元素赋值，合法        iArr[2] = -8;        System.out.println(Arrays.toString(iArr));        // 下面语句对iArr重新赋值,非法        // iArr = null;        // final修饰Person变量，p是一个引用变量        final Person p = new Person(45);        // 改变Person对象的age实例变量，合法        p.setAge(23);        System.out.println(p.getAge());        // 下面语句对P重新赋值，非法        // p = null;    }}
```

从上面程序中可以看出，使用 final 修饰的引用类型变量不能被重新赋值，但可以改变引用类型变量所引用对象的内容。例如上面 iArr 变量所引用的数组对象，final 修饰后的 iArr 变量不能被重新赋值，但 iArr 所引用数组的数组元素可以被改变。与此类似的是，p 变量也使用了 final 修饰，表明 p 变量不能被重新赋值，但 p 变量所引用 Person 对象的成员变量的值可以被改变。

注意：在使用 final 声明变量时，要求全部的字母大写，如 SEX，这点在开发中是非常重要的。

如果一个程序中的变量使用 public static final 声明，则此变量将称为全局变量，如下面的代码：

public static final String SEX= "女";

## final修饰方法

final 修饰的方法不可被重写，如果出于某些原因，不希望子类重写父类的某个方法，则可以使用 final 修饰该方法。

Java 提供的 Object 类里就有一个 final 方法 getClass()，因为 Java 不希望任何类重写这个方法，所以使用 final 把这个方法密封起来。但对于该类提供的 toString() 和 equals() 方法，都允许子类重写，因此没有使用 final 修饰它们。

下面程序试图重写 final 方法，将会引发编译错误。

```
public class FinalMethodTest {    public final void test() {    }}class Sub extends FinalMethodTest {    // 下面方法定义将出现编译错误，不能重写final方法    public void test() {    }}
```

上面程序中父类是 FinalMethodTest，该类里定义的 test() 方法是一个 final 方法，如果其子类试图重写该方法，将会引发编译错误。

对于一个 private 方法，因为它仅在当前类中可见，其子类无法访问该方法，所以子类无法重写该方法——如果子类中定义一个与父类 private 方法有相同方法名、相同形参列表、相同返回值类型的方法，也不是方法重写，只是重新定义了一个新方法。因此，即使使用 final 修饰一个 private 访问权限的方法，依然可以在其子类中定义与该方法具有相同方法名、相同形参列表、相同返回值类型的方法。

下面程序示范了如何在子类中“重写”父类的 private final 方法。

```
public class PrivateFinalMethodTest {    private final void test() {    }}class Sub extends PrivateFinalMethodTest {    // 下面的方法定义不会出现问题    public void test() {    }}
```

上面程序没有任何问题，虽然子类和父类同样包含了同名的 void test() 方法，但子类并不是重写父类的方法，因此即使父类的 void test() 方法使用了 final 修饰，子类中依然可以定义 void test() 方法。

final 修饰的方法仅仅是不能被重写，并不是不能被重载，因此下面程序完全没有问题。

```
public class FinalOverload {    // final 修饰的方法只是不能被重写，完全可以被重载    public final void test(){}    public final void test(String arg){}}
```

## final修饰类

final 修饰的类不能被继承。当子类继承父类时，将可以访问到父类内部数据，并可通过重写父类方法来改变父类方法的实现细节，这可能导致一些不安全的因素。为了保证某个类不可被继承，则可以使用 final 修饰这个类。

下面代码示范了 final 修饰的类不可被继承。

```
final class SuperClass {}class SubClass extends SuperClass {    //编译错误}
```

因为 SuperClass 类是一个 final 类，而 SubClass 试图继承 SuperClass 类，这将会引起编译错误。

## final 修饰符使用总结

#### 1. final 修饰类中的变量

表示该变量一旦被初始化便不可改变，这里不可改变的意思对基本类型变量来说是其值不可变，而对对象引用类型变量来说其引用不可再变。其初始化可以在两个地方：一是其定义处，也就是说在 final 变量定义时直接给其赋值；二是在构造方法中。这两个地方只能选其一，要么在定义时给值，要么在构造方法中给值，不能同时既在定义时赋值，又在构造方法中赋予另外的值。

#### 2. final 修饰类中的方法

说明这种方法提供的功能已经满足当前要求，不需要进行扩展，并且也不允许任何从此类继承的类来重写这种方法，但是继承仍然可以继承这个方法，也就是说可以直接使用。在声明类中，一个 final 方法只被实现一次。

#### 3. final 修饰类

表示该类是无法被任何其他类继承的，意味着此类在一个继承树中是一个叶子类，并且此类的设计已被认为很完美而不需要进行修改或扩展。

对于 final 类中的成员，可以定义其为 final，也可以不是 final。而对于方法，由于所属类为 final 的关系，自然也就成了 final 型。也可以明确地给 final 类中的方法加上一个 final，这显然没有意义。