# 字符类型

​	char型数据用来表示通常意义上"字符"(2字节).

​	Java中的所有字符都使用Unicode编码,故一个字符可以存储一个字母,一个汉字,或其他书面语的一个字符。

​	字符类型: `char`

提示：`char` 代表字符型，实际上字符型也是一种整数类型，相当于无符号整数类型。

字符型变量的三种**表现形式**:

- 字符常量是用单引号(`'` `'`)括起来的单个字符。


- Java中还允许使用[转义字符](../../../Appendix/ESC/README.md) `'\'`来将其后的字符转变为特殊字符型常量。                                          

- 直接使用Unicode值来表示字符型常量: `'\uXXXX’`。其中,XXXX代表一个十六进制整数。

**注意**：

- char类型**使用单引号`'`，且仅有一个字符**，要和双引号`"`的字符串类型区分开。
- char类型是可以进行运算的。因为它都对应有[Unicode码](../../../Appendix/ESC/README.md)。

```java
public class Main {
    public static void main(String[] args) {
        char c1 ='a'; 
        char c2= '中'; 
        char c3='9';	//用单引号括起来的单个字符
        
        char c3='\n';	// '\n'表示换行符
        c3 = '\t';	//\t水平制表符
        
        char c6 = '\u0122';	// \u000a表示\n
        char c7 = 97;
        System.out.println(c7); //97
        System.out.println(c6); //Ģ   
	}
}
```

