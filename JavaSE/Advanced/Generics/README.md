# 泛型

泛型是一种“代码模板”，可以用一套代码套用各种类型。泛型就是参数化类型，使用广泛的类型。

实现编写一次，万能匹配，又通过编译器保证了类型安全：这就是泛型。

![java-generics](https://www.liaoxuefeng.com/files/attachments/1290121955508289/l)

## 泛型的概念

泛型是JDK1.5出来的安全机制，保证了程序的安全性，并且**将运行时期异常提前到编译时期**，方便处理代码。

在[集合]()中，需要对集合中的内容进行操作或想存储相同类型时(存、取都需要同一类型时)，需要将默认的Object类强转为所需要的类，若类型不同则会产生异常。泛型正是解决此类问题的。

```java
ArrayList list = new ArrayList();
list.add("Hello");
// 获取到Object，必须强制转型为String:
String first = (String) list.get(0);
list.add(new Integer(123));
// ERROR: ClassCastException:
String second = (String) list.get(1);
```

## 泛型的使用

**基本格式**：

```java
变量、类、接口<具体的数据类型>
```

**例**：

使用[`ArrayList`]()时，如果不定义泛型类型时，泛型类型实际上就是`Object`：

```java
List list = new ArrayList();
list.add("Hello");
list.add("World");
String first = (String) list.get(0);
String second = (String) list.get(1);
```

**使用泛型**：

当我们定义泛型类型`<String>`后，`List<T>`的泛型接口变为强类型`List<String>`：

```java
List<String> list = new ArrayList<String>();
list.add("Hello");
list.add("World");
// 无强制转型:
String first = list.get(0);
String second = list.get(1);
```

当我们定义泛型类型`<Number>`后，`List<T>`的泛型接口变为强类型`List<Number>`：

```java
List<Number> list = new ArrayList<Number>();
list.add(new Integer(123));
list.add(new Double(12.34));
Number first = list.get(0);
Number second = list.get(1);
```

编译器如果能自动推断出泛型类型，就可以省略后面的泛型类型：

```java
List<Number> list = new ArrayList<Number>();
```

编译器看到泛型类型`List<Number>`就可以自动推断出后面的`ArrayList<T>`的泛型类型必须是`ArrayList<Number>`，因此，可以把代码简写为：

```java
// 可以省略后面的Number，编译器可以自动推断泛型类型：
List<Number> list = new ArrayList<>();
```

### 泛型类

编写泛型类比普通类要复杂。通常来说，泛型类一般用在集合类中，例如`ArrayList<T>`，我们很少需要编写泛型类。

**基本格式**：

```java
修饰符 class 类名称 <泛型标识、泛型标识，...> {
    private 泛型标识 变量名；
    ......
}
```

**泛型类的使用**：

```java
类名<具体的数据类型> 对象名 = new 类名<具体的数据类型>();
```

java 1.7以后，后边的<>中具体的数据类型可以省略不写：

```java
类名<具体的数据类型> 对象名 = new 类名<>();
```

**注意**：

- 泛型类，如果没有指定具体的数据类型，此时，操作类型是Object。
- 泛型的类型参数只能是引用类型，不能是基本数据类型。
- 泛型类型在逻辑上可以看成是多个不同的类型，但实际上是相同类型。

**例**：

```java
public class Test{
    public void static main(String[] args){
        A<String> a = new A<>();
        a.add("ll");
    }
}
class A<E>{
    public void add(E e){
        System.out.println(e);
    }
}
```

**例**：编写泛型类

1. 首先，按照某种类型，例如：`String`，来编写类，并标记所有的特定类型(String)：

   ```java
   public class Pair {
       private String first;
       private String last;
       public Pair(String first, String last) {
           this.first = first;
           this.last = last;
       }
       public String getFirst() {
           return first;
       }
       public String getLast() {
           return last;
       }
   }
   ```

2. 把特定类型`String`替换为`T`，并申明`<T>`：

   ```java 
   public class Pair<T> {
       private T first;
       private T last;
       public Pair(T first, T last) {
           this.first = first;
           this.last = last;
       }
       public T getFirst() {
           return first;
       }
       public T getLast() {
           return last;
       }
   }
   ```

#### 从泛型类派生子类

- 子类也是泛型类，子类和父类的泛型类型要保持一致

```java 
class ChildGeneric<T> extends Generic<T>
```

- 子类不是泛型类，父类要明确泛型类的数据类型

```java
class ChildGeneric extends Generic
```

##### 子类使用泛型

如果父类不指定数据类型的话，默认为Object。当父类指定数据类型的时候，子类和父类的泛型类型要保持一致，当和子类指定不同的数据类型的时候就会报错。

> 父类

```java
public class Parent<E> {
 
    private E value;
 
    public E getValue() {
        return value;
    }
 
    public void setValue(E value) {
        this.value = value;
    }
}
```

> 子类

```java
public class ChildFirst<T> extends Parent<T> {
//public class ChildFirst<T> extends Parent{}  (默认为Object)
    @Override
    public T getValue() {
        return super.getValue();
    }
}
```

##### 子类没有使用泛型

当子类没有使用泛型的时候，父类的泛型类操作的是Object。在创建子类对象的时候，无法确定父类的泛型使用的数据类型，需要明确数据类型。

> 子类

```java
//public class ChildFirst extends Parent {} //默认Object
//public class ChildFirst extends Parent<T> {}	//无法确定父类类型
public class ChildFirst extends Parent<String> {}//明确数据类型
```

### 泛型方法

使用泛型的方法叫泛型方法。

**基本格式**：

```java
修饰符 <具体的数据类型> 返回值类型 方法名(参数){}
```

**注意**：泛型方法的定义与其所在的类是否是泛型类是没有任何关系的，所在的类可以是泛型类，也可以不是泛型类。

**例**：

```java
//普通类中定义泛型方法
class Demo {
    public <T> T fun(T t) {  //可以接收任意类型的数据
        return t;
    }
}

//泛型类中定义泛型方法
class S<E> {
    public void add(E e) {
        System.out.println(e);
    }
}
```

#### 静态方法

静态方法无法访问类上定义的泛型；如果静态方法操作的引用数据类型不确定的时候，必须要将泛型定义在方法上。

即：如果静态方法要使用泛型的话，必须将静态方法也定义成泛型方法 。

**例**：

```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() { ... }
    public T getLast() { ... }

    // 对静态方法使用<T>:
    public static Pair<T> create(T first, T last) {
        return new Pair<T>(first, last);
    }
}
```

上述代码会导致编译错误，我们无法在静态方法`create()`的方法参数和返回类型上使用泛型类型`T`。

可以在`static`修饰符后面加一个`<T>`，编译就能通过：

```
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() { ... }
    public T getLast() { ... }

    // 可以编译通过:
    public static <T> Pair<T> create(T first, T last) {
        return new Pair<T>(first, last);
    }
}
```

但实际上，这个`<T>`和`Pair<T>`类型的`<T>`已经没有任何关系了。

对于静态方法，我们可以单独改写为“泛型”方法，只需要使用另一个类型即可。对于上面的`create()`静态方法，我们应该把它改为另一种泛型类型，例如，`<K>`：

```
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() { ... }
    public T getLast() { ... }

    // 静态泛型方法应该使用其他类型区分:
    public static <K> Pair<K> create(K first, K last) {
        return new Pair<K>(first, last);
    }
}
```

这样才能清楚地将静态方法的泛型类型和实例类型的泛型类型区分开。

### 泛型接口

在定义一个接口的时候如果某些类型不能确定，那么就使用占位符标记，在具体使用的时候再指定泛型的类型。

直接在实现类中指定泛型的具体类型，在实现类中继续使用泛型，在实例化实现类对象的时候指定泛型的具体类型，在接口继承接口中指定泛型的具体类型。

**基本格式**：

```java
修饰符 interface 接口名<具体的数据类型>{}
```

**泛型接口的使用**：

- 实现类不是泛型类，接口要明确数据类型
- 实现类也是泛型类，实现类和接口的泛型类型要一致

**注意**：

- 可以在接口中定义泛型类型，实现此接口的类必须实现正确的泛型类型。
- 不能泛型静态常量

**例**：

> 接口

```java
public interface MyIterface<T> {
    public final static String name = "yuan";
    public abstract T server(T t);
}
```

> 实现类(对泛型接口实现类的时就确定接口的泛型类型)

```java
public class MyImplement implements MyIterface<String> {
    @Override
    public String server(String s) {
        System.out.println(s);
        return s;
    }
}
```

> 实现类(如果实现接口的时候不确定类型T，那就实现一个泛型类)

```java 
public class MyImplement2<T> implements MyIterface<T> {
    @Override
    public T server(T t) {
        System.out.println(t);
        return t;
    }
}
```

> 代码

```java
public class Test {
    public static void main(String[] args) {
        MyImplement myImplement = new MyImplement();
        myImplement.server("你好啊");//你好啊

        MyImplement2<Integer> myimplement2 = new MyImplement2<>();
        myimplement2.server(1000);//1000
    }
}
```

**注意**：

- new一个实现类一的对象后可以直接调用重写的`server()`方法，在方法中传入的参数必须与实现接口的泛型一样

- new一个实现类二的对象时需要指明泛型类型，再根据泛型类型调用重写的`server()`方法

## 多个泛型类型

泛型还可以定义多种类型。

**例**：

```java
public class Pair<T, K> {
    private T first;
    private K last;
    public Pair(T first, K last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() { ... }
    public K getLast() { ... }
}
```

使用的时候，需要指出两种类型：

```java
Pair<String, Integer> p = new Pair<>("test", 123);
```

Java标准库的`[Map<K, V>`]()就是使用两种泛型类型的例子。它对Key使用一种类型，对Value使用另一种类型。

## 向上转型

在Java标准库中的`ArrayList<T>`实现了`List<T>`接口，它可以向上转型为`List<T>`：

```java
public class ArrayList<T> implements List<T> {
    ...
}

List<String> list = new ArrayList<String>();
```

即类型`ArrayList<T>`可以向上转型为`List<T>`。

**注意**：不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`或`List<Number>`。

假设`ArrayList<Integer>`可以向上转型为`ArrayList<Number>`：

```java 
// 创建ArrayList<Integer>类型：
ArrayList<Integer> integerList = new ArrayList<Integer>();
// 添加一个Integer：
integerList.add(new Integer(123));
// “向上转型”为ArrayList<Number>：
ArrayList<Number> numberList = integerList;
// 添加一个Float，因为Float也是Number：
numberList.add(new Float(12.34));
// 从ArrayList<Integer>获取索引为1的元素（即添加的Float）：
Integer n = integerList.get(1); // ClassCastException!
```

将一个`ArrayList<Integer>`转型为`ArrayList<Number>`类型后，这个`ArrayList<Number>`就可以接受`Float`类型，因为`Float`是`Number`的子类。但是，`ArrayList<Number>`实际上和`ArrayList<Integer>`是同一个对象，也就是`ArrayList<Integer>`类型，它不可能接受`Float`类型， 所以在获取`Integer`的时候将产生`ClassCastException`。

实际上，编译器为了避免这种错误，根本就不允许把`ArrayList<Integer>`转型为`ArrayList<Number>`。

 `ArrayList<Integer>`和`ArrayList<Number>`两者完全没有继承关系。

**注意**：泛型的继承关系：可以把`ArrayList<Integer>`向上转型为`List<Integer>`（`T`不能变！），但不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`（`T`不能变成父类）。

## 泛型的优点

- 使赋值更加灵活。


- 泛型避免强转，避免定义Object 使用时需要强转。


- 使用时不必对类型进行强制转换，它通过编译器对类型进行检查

- 指定集合存储的数据类型

- 将运行时期异常提前到编译时期

- 泛型只有编译时期有，运行时会擦除(只对javac有效，对java命令无效)


## 泛型的通配符

在java中，数组是可以协变的，比如`dog extends Animal`，那么`Animal[]` 与`dog[]`是兼容的。而集合是不能协变的，也就是说`List<Animal>`不是`List<dog>`的父类，这时候就可以用到通配符了。

### 无边界通配符

无边界的通配符(`Unbounded Wildcards`),，就是`<?>`, 比如`List<?>`.
**作用**：让泛型能够接受未知类型的数据.。

### 固定上边界通配符(上限限定)

使用固定上边界的通配符的泛型, 就能够接受指定类及其子类类型的数据。要声明使用该类通配符, 采用<? extends E>的形式, 这里的E就是该泛型的上边界. 注意: 这里虽然用的是extends关键字, 却不仅限于继承了父类E的子类, 也可以代指显现了接口E的类. 



泛型的上限限定：`? extends E` 代表使用的泛型只能是E的子类或者本身

可以传递该类本身，也可以传递super的子类，不能传递super的父类

```
? extends super
```

extends通配符

假设我们定义了`Pair<T>`：

```
public class Pair<T> { ... }
```

然后，我们又针对`Pair<Number>`类型写了一个静态方法，它接收的参数类型是`Pair<Number>`：

```
public class PairHelper {
    static int add(Pair<Number> p) {
        Number first = p.getFirst();
        Number last = p.getLast();
        return first.intValue() + last.intValue();
    }
}
```

上述代码是可以正常编译的。使用的时候，我们传入：

```
int sum = PairHelper.add(new Pair<Number>(1, 2));
```

注意：传入的类型是`Pair<Number>`，实际参数类型是`(Integer, Integer)`。

既然实际参数是`Integer`类型，试试传入`Pair<Integer>`：

```
public class Main {
}

class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}
```

直接运行，会得到一个编译错误：

```
incompatible types: Pair<Integer> cannot be converted to Pair<Number>
```

原因很明显，因为`Pair<Integer>`不是`Pair<Number>`的子类，因此，`add(Pair<Number>)`不接受参数类型`Pair<Integer>`。

但是从`add()`方法的代码可知，传入`Pair<Integer>`是完全符合内部代码的类型规范，因为语句：

```
Number first = p.getFirst();
Number last = p.getLast();
```

实际类型是`Integer`，引用类型是`Number`，没有问题。问题在于方法参数类型定死了只能传入`Pair<Number>`。

有没有办法使得方法参数接受`Pair<Integer>`？办法是有的，这就是使用`Pair<? extends Number>`使得方法接收所有泛型类型为`Number`或`Number`子类的`Pair`类型。我们把代码改写如下：

```
public class Main {
}

class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}
```

这样一来，给方法传入`Pair<Integer>`类型时，它符合参数`Pair<? extends Number>`类型。这种使用`<? extends Number>`的泛型定义称之为上界通配符（Upper Bounds Wildcards），即把泛型类型`T`的上界限定在`Number`了。

除了可以传入`Pair<Integer>`类型，我们还可以传入`Pair<Double>`类型，`Pair<BigDecimal>`类型等等，因为`Double`和`BigDecimal`都是`Number`的子类。

如果我们考察对`Pair<? extends Number>`类型调用`getFirst()`方法，实际的方法签名变成了：

```
<? extends Number> getFirst();
```

即返回值是`Number`或`Number`的子类，因此，可以安全赋值给`Number`类型的变量：

```
Number x = p.getFirst();
```

然后，我们不可预测实际类型就是`Integer`，例如，下面的代码是无法通过编译的：

```
Integer x = p.getFirst();
```

这是因为实际的返回类型可能是`Integer`，也可能是`Double`或者其他类型，编译器只能确定类型一定是`Number`的子类（包括`Number`类型本身），但具体类型无法确定。

我们再来考察一下`Pair<T>`的`set`方法：

```
public class Main {
}

class Pair<T> {
    private T first;
    private T last;

    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }

    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
    public void setFirst(T first) {
        this.first = first;
    }
    public void setLast(T last) {
        this.last = last;
    }
}
```

不出意外，我们会得到一个编译错误：

```
incompatible types: Integer cannot be converted to CAP#1
where CAP#1 is a fresh type-variable:
    CAP#1 extends Number from capture of ? extends Number
```

编译错误发生在`p.setFirst()`传入的参数是`Integer`类型。有些童鞋会问了，既然`p`的定义是`Pair<? extends Number>`，那么`setFirst(? extends Number)`为什么不能传入`Integer`？

原因还在于擦拭法。如果我们传入的`p`是`Pair<Double>`，显然它满足参数定义`Pair<? extends Number>`，然而，`Pair<Double>`的`setFirst()`显然无法接受`Integer`类型。

这就是`<? extends Number>`通配符的一个重要限制：方法参数签名`setFirst(? extends Number)`无法传递任何`Number`的子类型给`setFirst(? extends Number)`。

这里唯一的例外是可以给方法参数传入`null`：

```
p.setFirst(null); // ok, 但是后面会抛出NullPointerException
p.getFirst().intValue(); // NullPointerException
```

extends通配符的作用

如果我们考察Java标准库的`java.util.List<T>`接口，它实现的是一个类似“可变数组”的列表，主要功能包括：

```
public interface List<T> {
    int size(); // 获取个数
    T get(int index); // 根据索引获取指定元素
    void add(T t); // 添加一个新元素
    void remove(T t); // 删除一个已有元素
}
```

现在，让我们定义一个方法来处理列表的每个元素：

```
int sumOfList(List<? extends Integer> list) {
    int sum = 0;
    for (int i=0; i<list.size(); i++) {
        Integer n = list.get(i);
        sum = sum + n;
    }
    return sum;
}
```

为什么我们定义的方法参数类型是`List<? extends Integer>`而不是`List<Integer>`？从方法内部代码看，传入`List<? extends Integer>`或者`List<Integer>`是完全一样的，但是，注意到`List<? extends Integer>`的限制：

- 允许调用`get()`方法获取`Integer`的引用；
- 不允许调用`set(? extends Integer)`方法并传入任何`Integer`的引用（`null`除外）。

因此，方法参数类型`List<? extends Integer>`表明了该方法内部只会读取`List`的元素，不会修改`List`的元素（因为无法调用`add(? extends Integer)`、`remove(? extends Integer)`这些方法。换句话说，这是一个对参数`List<? extends Integer>`进行只读的方法（恶意调用`set(null)`除外）。

使用extends限定T类型

在定义泛型类型`Pair<T>`的时候，也可以使用`extends`通配符来限定`T`的类型：

```
public class Pair<T extends Number> { ... }
```

现在，我们只能定义：

```
Pair<Number> p1 = null;
Pair<Integer> p2 = new Pair<>(1, 2);
Pair<Double> p3 = null;
```

因为`Number`、`Integer`和`Double`都符合`<T extends Number>`。

非`Number`类型将无法通过编译：

```
Pair<String> p1 = null; // compile error!
Pair<Object> p2 = null; // compile error!
```

因为`String`、`Object`都不符合`<T extends Number>`，因为它们不是`Number`类型或`Number`的子类。

总结

使用类似`<? extends Number>`通配符作为方法参数时表示：

- 方法内部可以调用获取`Number`引用的方法，例如：`Number n = obj.getFirst();`；
- 方法内部无法调用传入`Number`引用的方法（`null`除外），例如：`obj.setFirst(Number n);`。

即一句话总结：使用`extends`通配符表示可以读，不能写。

使用类似`<T extends Number>`定义泛型类时表示：

- 泛型类型限定为`Number`以及`Number`的子类。

### 固定下边界通配符(下限限定)

使用固定下边界的通配符的泛型, 就能够接受指定类及其父类类型的数据. 要声明使用该类通配符, 采用<? super E>的形式, 这里的E就是该泛型的下边界. 注意: 你可以为一个泛型指定上边界或下边界, 但是不能同时指定上下边界.

泛型的下限限定：？ super E 代表使用的泛型只能是E的父类或者本身

```
? super 类
```

![image-20221026225711756](D:/Data/typora/photo/image-20221026225711756.png)

![image-20221026225731374](D:/Data/typora/photo/image-20221026225731374.png)

![image-20221026225743251](D:/Data/typora/photo/image-20221026225743251.png)

## 泛型常用字母



![image-20221026223212672](D:/Data/typora/photo/image-20221026223212672.png)
