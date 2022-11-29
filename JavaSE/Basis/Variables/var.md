# var变量

有些时候，类型的名字太长，写起来比较麻烦。例如：

```java
StringBuilder sb = new StringBuilder();
```

这个时候，如果想省略变量类型，可以使用var关键字：

```java
var sb = new StringBuilder();
```

编译器会根据赋值语句自动推断出变量`sb`的类型是`StringBuilder`。对编译器来说，语句：

```java
var sb = new StringBuilder();
```

实际上会自动变成：

```java
StringBuilder sb = new StringBuilder();
```

因此，使用var定义变量，仅仅是少写了变量类型而已。

```java
public class var类型 {
    public static void main(String[] args) {
        var ss = new StringBuilder();
        ss.name ="nn";
        ss.age = 15;
        System.out.println(ss.name + ss.age);
    }
}
class StringBuilder{
    String name;
    int age;
}
```