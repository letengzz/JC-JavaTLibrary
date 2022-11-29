# 集合介绍

在编程时，可以使用[数组](../../Basis/Reference_Types/Array/README.md)来保存多个对象，但**数组长度不可变化**，一旦在初始化数组时指定了数组长度，这个数组长度就是不可变的。如果需要保存数量变化的数据，数组就有点无能为力了。而且**数组无法保存具有映射关系的数据**，如成绩表为语文——79，数学——80，这种数据看上去像两个数组，但这两个数组的元素之间有一定的关联关系。

为了保存数量不确定的数据，以及保存具有映射关系的数据(也被称为关联数组)，Java 提供了集合类。**集合类主要负责保存、盛装其他数据**，因此集合类也被称为容器类。Java 所有的集合类都位于 `java.util` 包下，提供了一个表示和操作对象集合的统一构架，包含大量集合接口，以及这些接口的实现类和操作它们的算法。

集合类和数组不一样，数组元素既可以是基本类型的值，也可以是对象(实际上保存的是对象的引用变量)，而集合里只能保存对象(实际上只是保存对象的引用变量，但通常习惯上认为集合里保存的是对象)。

Java 集合类型分为 [Collection](Collection/README.md) 和 [Map](Map/README.md)，它们是 Java 集合的根接口，这两个接口又包含了一些子接口或实现类：

![图片6](D:/Data/typora/photo/%E5%9B%BE%E7%89%876-16603965218745.png)

![图片7](D:/Data/typora/photo/%E5%9B%BE%E7%89%877-16603981110697.png)

**注**：黄色块为集合的接口，蓝色块为集合的实现类。

![图片4](D:/Data/typora/photo/%E5%9B%BE%E7%89%874-16602249245011.png)
对于 [Set](Collection/Set/README.md)、[List](Collection/List/README.md)、[Queue](Collection/Queue/README.md) 和 [Map](Map/README.md) 这 4 种集合，Java 最常用的实现类分别是 [HashSet](Class/HashSet.md)、[TreeSet](Class/TreeSet.md)、[ArrayList](Class/ArrayList.md)、[ArrayDueue](Class/ArrayDueue.md)、[LinkedList](Class/LinkedList.md)和 [HashMap](Class/HashMap.md)、[TreeMap](Class/TreeMap.md)等。

![图片5](D:/Data/typora/photo/%E5%9B%BE%E7%89%875-16603093454215.png)