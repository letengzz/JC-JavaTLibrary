# 变量的分类

**按数据类型分类**：

​	对于每一种数据都定义了明确的具体数据类型(强类型语言)，在内存中分配了不同大写的内存空间

![clipboard](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207272117848.png)

**按声明的位置分类**：

- 在方法体外，类体内声明的变量称为[成员变量](member_variable.md)。

- 在方法体内部声明的变量称为[局部变量](local_variable.md)。

![clipboard1](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207272117461.png)

**注意**：二者在初始化值方面的异同:

- 同:都有生命周期。

- 异:局部变量除形参外,需显式初始化(局部变量在使用前需要初始化)。

![clipboard3](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207272119104.png)