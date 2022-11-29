# 布尔类型

​	Java虚拟机中没有任何供boolean值专用的字节码指令，Java语言表达所操作的 boolean值，在编译之后都使用java虚拟机中的int数据类型来代替：true用1表示，false 用0表示。———《java虚拟机规范 8版》

​	布尔型: `boolean`

boolean 类型用来判断逻辑条件，一般用于程序流程控制： 

- [if条件控制语句](../Process_Control/Branch_Structure/if_else.md)； 
- [while循环控制语句](../Process_Control/Loop_Structure/while.md)； 
- [do-while循环控制语句](../Process_Control/Loop_Structure/do_while.md)； 
- [for循环控制语句](../Process_Control/Loop_Structure/for.md)； 

**注意**：

- boolean类型数据**只允许取值`true`和`false`，无`null`。**


- **不可以使用0或非 0 的整数替代`false`和`true`，这点和C语言不同。** 

- Java语言对布尔类型的存储并没有做规定，因为理论上存储布尔类型只需要1 `bit`，但是通常JVM内部会把`boolean`表示为4字节整数。


```java
public class Main {
    public static void main(String[] args) {
		boolean b1 = true;
		boolean b2 = false;
		boolean isGreater = 5 > 3; // 计算结果为true
		int age = 12;
		boolean isAdult = age >= 18; // 计算结果为false

        //通常在条件判断 循环结构中使用
        boolean isMarried = true;
        if (isMarried){
            System.out.println("你好");
        }else {
            System.out.println("你不好");
        }	//你好
        
    }
}
```



