# 内部类

在类内部可定义成员变量和方法，且在类内部也可以定义另一个类。如果在类 Outer 的内部再定义一个类 Inner，此时类 Inner 就称为内部类(或称为嵌套类、`Nested Class`)，而类 Outer 则称为外部类(或称为宿主类)。

内部类可以很好地实现隐藏，一般的非内部类是不允许有 private 与 protected 权限的，但内部类可以。**内部类拥有外部类的所有元素的访问权限**。

内部类可以分为：[实例内部类]()、[静态内部类]()和[成员内部类]()，每种内部类都有它特定的一些特点。

在类 A 中定义类 B，那么类 B 就是内部类，也称为嵌套类，相对而言，类 A 就是外部类。如果有多层嵌套，例如类 A 中有内部类 B，而类 B 中还有内部类 C，那么通常将最外层的类称为顶层类(或者顶级类)。

![img](http://c.biancheng.net/uploads/allimg/181023/3-1Q02311045J93.jpg)

**内部类的特点**：

1. 内部类仍然是一个独立的类，在编译之后内部类会被编译成独立的`.class`文件，但是前面冠以外部类的类名和`$`符号。
2. 内部类不能用普通的方式访问。内部类是外部类的一个成员，因此内部类可以自由地访问外部类的成员变量，无论是否为 private 的。
3. 内部类声明成静态的，就不能随便访问外部类的成员变量，仍然是只能访问外部类的静态成员变量。

**说明**：

- 外部类只有两种访问级别：[public]() 和[default]()，内部类则有 4 种访问级别：[public]()、[protected]()、 [private]() 和[default]()。

- 在外部类中可以直接通过内部类的类名访问内部类：

  ```java
  InnerClass ic = new InnerClass();    // InnerClass为内部类的类名
  ```

- 在外部类以外的其他类中则需要通过内部类的完整类名访问内部类：

  ```java
  Test.InnerClass ti = newTest().new InnerClass();    // Test.innerClass是内部类的完整类名
  ```

- 内部类与外部类不能重名。

**提示**：内部类的很多访问规则可以参考变量和方法。另外使用内部类可以使程序结构变得紧凑，但是却在一定程度上破坏了 Java 面向对象的思想。

**例**：

```java
public class Test {    
    public class InnerClass {        
        public int getSum(int x,int y) {            
            return x + y;        
        }    
    }    
    public static void main(String[] args) {        
        Test.InnerClass ti = new Test().new InnerClass();        
        int i = ti.getSum(2,3);        
        System.out.println(i);    // 输出5    
    }
}
```

- [Java实例内部类](http://c.biancheng.net/view/1025.html)
- [Java静态内部类](http://c.biancheng.net/view/1026.html)
- [Java局部内部类](http://c.biancheng.net/view/1028.html)

## 实例内部类

实例内部类是指没有用 static 修饰的内部类，也称为非静态内部类。

**基本结构**：

```java
public class Outer {    
    class Inner {        
        // 实例内部类    
    }
}
```

**说明**：实例内部类和普通Class相比，除了能引用外部类实例外，还有一个额外的“特权”，就是可以修改外部类的`private`字段，因为内部类的作用域在外部类内部，所以能访问外部类的`private`字段和方法。

**注意**：Java编译器编译后的`.class`文件可以发现，`Outer`类被编译为`Outer.class`，而`Inner`类被编译为`Outer$Inner.class`。

**实例内部类特点**：

1. 实例内部类的实例在外部类的静态方法和外部类以外的其他类中，必须依附于外部类的实例来创建。

   ```java
   public class Outer {    
       class Inner1 {    
       }    
       Inner1 i = new Inner1(); 
       // 不需要创建外部类实例    
       public void method1() {        
           Inner1 i = new Inner1(); 
           // 不需要创建外部类实例    
       }    
       public static void method2() {        
           Inner1 i = new Outer().new inner1(); 
           // 需要创建外部类实例    
       }    
       class Inner2 {        
           Inner1 i = new Inner1(); 
           // 不需要创建外部类实例    
       }
   }
   class OtherClass {    
       Outer.Inner i = new Outer().new Inner(); 
       // 需要创建外部类实例
   }
   ```

2. 在实例内部类中，可以访问外部类的所有成员。

   ```java
   public class Outer {    
       public int a = 100;    
       static int b = 100;    
       final int c = 100;    
       private int d = 100;    
       public String method1() {        
           return "实例方法1";    
       }    
       public static String method2() {        
           return "静态方法2";    
       }    
       class Inner {        
           int a2 = a + 1; // 访问public的a        
           int b2 = b + 1; // 访问static的b        
           int c2 = c + 1; // 访问final的c        
           int d2 = d + 1; // 访问private的d        
           String str1 = method1(); // 访问实例方法method1        
           String str2 = method2(); // 访问静态方法method2    
       }    
       public static void main(String[] args) {        
           Inner i = new Outer().new Inner(); // 创建内部类实例        
           System.out.println(i.a2); // 输出101        
           System.out.println(i.b2); // 输出101        
           System.out.println(i.c2); // 输出101        
           System.out.println(i.d2); // 输出101        
           System.out.println(i.str1); // 输出实例方法1        
           System.out.println(i.str2); // 输出静态方法2    
       }
   }
   ```

**提示**：如果有多层嵌套，则内部类可以访问所有外部类的成员。

3. 在外部类中不能直接访问内部类的成员，而必须通过内部类的实例去访问。如果类 A 包含内部类 B，类 B 中包含内部类 C，则在类 A 中不能直接访问类 C，而应该通过类 B 的实例去访问类 C。

4. 外部类实例与内部类实例是一对多的关系，也就是说一个内部类实例只对应一个外部类实例，而一个外部类实例则可以对应多个内部类实例。

5. 如果实例内部类 B 与外部类 A 包含有同名的成员 t，则在类 B 中 t 和 this.t 都表示 B 中的成员 t，而 A.this.t 表示 A 中的成员 t。

   Inner Class除了有一个`this`指向它自己，还隐含地持有一个Outer Class实例，可以用`Outer.this`访问这个实例。所以，实例化一个Inner Class不能脱离Outer实例。

   ```java
   public class Outer {    
       int a = 10;    
       class Inner {        
           int a = 20;        
           int b1 = a;        
           int b2 = this.a;        
           int b3 = Outer.this.a;    
       }    
       public static void main(String[] args) {        
           Inner i = new Outer().new Inner();        
           System.out.println(i.b1); // 输出20        
           System.out.println(i.b2); // 输出20        
           System.out.println(i.b3); // 输出10    
       }
   }
   ```

6. 在实例内部类中不能定义 static 成员，除非同时使用 final 和 static 修饰。

## 匿名内部类

匿名类是指没有类名的内部类，必须在创建时使用 new 语句来声明类。

**语法形式**：

```java
new <类或接口>() {    
    // 类的主体
};
```

这种形式的 new 语句声明一个新的匿名类，它对一个给定的类进行扩展，或者实现一个给定的接口。使用匿名类可使代码更加简洁、紧凑，模块化程度更高。

匿名类实现方式：

- 继承一个类，重写其方法。
- 实现一个接口（可以是多个），实现其方法。

**例**：

```java
public class Out {    
    void show() {        
        System.out.println("调用 Out 类的 show() 方法");    
    }
}
public class TestAnonymousInterClass {    
    // 在这个方法中构造一个匿名内部类    
    private void show() {        
        Out anonyInter = new Out() {            
            // 获取匿名内部类的实例            
            void show() {                
                System.out.println("调用匿名类中的 show() 方法");
            }        
        };        
        anonyInter.show();    
    }    
    public static void main(String[] args) { 
        TestAnonymousInterClass test = new TestAnonymousInterClass();
        test.show();    
    }
}
```

输出结果：

> 调用匿名类中的 show() 方法

从输出结果可以看出，匿名内部类有自己的实现。

**提示**：匿名内部类实现一个接口的方式与实现一个类的方式相同。

匿名类有如下特点：

1）匿名类和局部内部类一样，可以访问外部类的所有成员。如果匿名类位于一个方法中，则匿名类只能访问方法中 final 类型的局部变量和参数。

```
public static void main(String[] args) {    int a = 10;    final int b = 10;    Out anonyInter = new Out() {        void show() {            // System.out.println("调用了匿名类的 show() 方法"+a);    // 编译出错            System.out.println("调用了匿名类的 show() 方法"+b);    // 编译通过        }    };    anonyInter.show();}
```

> 从 [Java](http://c.biancheng.net/java/) 8 开始添加了 Effectively final 功能，在 Java 8 及以后的版本中代码第 6 行不会出现编译错误，详情可点击《[Java8新特性之Effectively final](http://c.biancheng.net/view/6564.html)》进行学习。

2）匿名类中允许使用非静态代码块进行成员初始化操作。

```
Out anonyInter = new Out() {    int i; {    // 非静态代码块        i = 10;    //成员初始化    }    public void show() {        System.out.println("调用了匿名类的 show() 方法"+i);    }};
```

3）匿名类的非静态代码块会在父类的构造方法之后被执行。

------

定义`Inner Class`的方法，它不需要在Outer Class中明确地定义这个Class，而是在方法内部，通过匿名类(`Anonymous Class`)来定义：

```java 
public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer("Nested");
        outer.asyncHello();
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    void asyncHello() {
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("Hello, " + Outer.this.name);
            }
        };
        new Thread(r).start();
    }
}
```

观察`asyncHello()`方法，我们在方法内部实例化了一个`Runnable`。`Runnable`本身是接口，接口是不能实例化的，所以这里实际上是定义了一个实现了`Runnable`接口的匿名类，并且通过`new`实例化该匿名类，然后转型为`Runnable`。在定义匿名类的时候就必须实例化它，定义匿名类的写法如下：

```java 
Runnable r = new Runnable() {
    // 实现必要的抽象方法...
};
```

匿名类和Inner Class一样，可以访问Outer Class的`private`字段和方法。之所以我们要定义匿名类，是因为在这里我们通常不关心类名，比直接定义Inner Class可以少写很多代码。

观察Java编译器编译后的`.class`文件可以发现，`Outer`类被编译为`Outer.class`，而匿名类被编译为`Outer$1.class`。如果有多个匿名类，Java编译器会将每个匿名类依次命名为`Outer$1`、`Outer$2`、`Outer$3`……

除了接口外，匿名类也完全可以继承自普通类：

```java 
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, String> map1 = new HashMap<>();
        HashMap<String, String> map2 = new HashMap<>() {}; // 匿名类!
        HashMap<String, String> map3 = new HashMap<>() {
            {
                put("A", "1");
                put("B", "2");
            }
        };
        System.out.println(map3.get("A"));
    }
}
```

`map1`是一个普通的`HashMap`实例，但`map2`是一个匿名类实例，只是该匿名类继承自`HashMap`。`map3`也是一个继承自`HashMap`的匿名类实例，并且添加了`static`代码块来初始化数据。观察编译输出可发现`Main$1.class`和`Main$2.class`两个匿名类文件。

## 静态内部类

和Inner Class类似，但是使用`static`修饰，称为**静态内部类**(`Static Nested Class`)：

```java 
public class Main {
    public static void main(String[] args) {
        Outer.StaticNested sn = new Outer.StaticNested();
        sn.hello();
    }
}

class Outer {
    private static String NAME = "OUTER";

    private String name;

    Outer(String name) {
        this.name = name;
    }

    static class StaticNested {
        void hello() {
            System.out.println("Hello, " + Outer.NAME);
        }
    }
}
```

用`static`修饰的内部类和Inner Class有很大的不同，它不再依附于`Outer`的实例，而是一个完全独立的类，因此无法引用`Outer.this`，但它可以访问`Outer`的`private`静态字段和静态方法。如果把`StaticNested`移到`Outer`之外，就失去了访问`private`的权限。

## 总结

Java的内部类可分为`Inner Class`、`Anonymous Class`和`Static Nested Class`三种：

- `Inner Class`和`Anonymous Class`本质上是相同的，都必须依附于`Outer Class`的实例，即隐含地持有`Outer.this`实例，并拥有Outer Class的`private`访问权限；
- `Static Nested Class`是独立类，但拥有`Outer Class`的`private`访问权限。