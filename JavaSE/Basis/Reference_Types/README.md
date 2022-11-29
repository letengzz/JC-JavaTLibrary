# 引用类型

引用数据类型建立在基本数据类型的基础上，包括[数组](Array/README.md)、[类](../../Advanced/Object_Oriented/Class/README.md)和[接口](../../Advanced/Object_Oriented/Class/interface.md)。引用数据类型是由用户自定义，用来限制其他数据的类型。另外，Java 语言中不支持 C++ 中的指针类型、结构类型、联合类型和枚举类型。

引用类型还有一种特殊的 `null` 类型。所谓引用数据类型就是对一个对象的引用，对象包括实例和数组两种。实际上，引用类型变量就是一个指针，它内部存储一个"地址"，指向某个对象在内存的位置。只是 Java 语言里不再使用指针这个说法。

空类型(`null type`)就是 `null` 值的类型，这种类型没有名称。因为 `null` 类型没有名称，所以不可能声明一个 `null` 类型的变量或者转换到 `null` 类型。

空引用(`null`)是 `null` 类型变量唯一的值。空引用(`null`)可以转换为任何引用类型。

在实际开发中，程序员可以忽略 `null` 类型，假定 `null` 只是引用类型的一个特殊直接量。

**注意**：

- 引用数据类型的大小统一为4字节(64位机器为8字节，64位如果使用指针压缩就是 4字节)，记录的是其引用对象的地址。
- 空引用(`null`)只能被转换成引用类型，不能转换成基本类型，因此不要把一个 `null` 值赋给基本数据类型的变量。
- [数组`array`](Array/README.md)
- [类`class`](../../Advanced/Object_Oriented/Class/README.md)
- [`String`关键字](../../Advanced/Object_Oriented/Class/String/README.md)
- [接口`interface`](../../Advanced/Object_Oriented/Class/interface.md)
