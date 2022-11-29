# 静态变量(类变量 `static variable`)

​	使用`static`定义。从属于类，生命周期伴随类始终，从类的加载到卸载。

```java
权限修饰符 static 数据类型 变量名 = 变量值;
```

**注意**：

- 如果不自行初始化，与成员变量相同会自动初始化该类型的默认初始值。

  ```java
  class Person {
      public String name;
      public int age;
      // 定义静态字段number:
      public static int number;
  }
  ```

**详细介绍静态变量**：[Here](../../Advanced/Object_Oriented/Keyword/static.md)

