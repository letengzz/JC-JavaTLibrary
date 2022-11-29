# 成员变量(实例变量 `member variable`)

​	方法外部、类的内部定义的变量。属于对象，生命周期伴随对象始终。

 定义变量的**格式**:

```
数据类型 变量名 = 变量值;
```

**实例变量**：不以static修饰的。

**类变量**：以static修饰的。

**注意**：

* 如果不自行初始化，它会自动初始化该类型的默认初始值。

* 变量都有其对应的作用域
  在类中声明的位置：直接定义在一对`{` `}`中

* 权限修饰符可以在声明属性时，指明其权限 使用权限修饰符

  常用的[权限修饰符](../../Advanced/Object_Oriented/Keyword/README.md)：`private`、`public`、缺-省、`protected`  -->封装性

* 根据其类型，有默认初始化值

  ![图片3](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207222133532.png)

* 在内存中加载到堆空间中（非`static`）
