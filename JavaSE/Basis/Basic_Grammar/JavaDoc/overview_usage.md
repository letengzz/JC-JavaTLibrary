# Javadoc概述

Java 文档注释是用来生成 API 文档的。Java 文档注释以`/**`开始，并以`*/`结束，可以通过 Javadoc 生成 API 帮助文档，Java 帮助文档主要用来说明类、接口、方法、成员变量、构造器和内部类。

Javadoc (Java API 文档生成器)是一种从源代码中的文档注释生成 HTML 格式的 API 文档的工具。

Javadoc 是 Sun 公司提供的一种工具，它只处理文档源文件在类、接口、方法、成员变量、构造器和内部类之前的注释，忽略其他地方的文档注释，然后形成一个和源代码配套的 API 帮助文档。也就是说，只要在编写程序时在文档注释中以一套特定的标签注释，在程序编写完成后，通过 Javadoc 就形成了程序的 API 帮助文档。API 帮助文档相当于产品说明书，说明书只需要介绍那些供用户使用的部分，所以 **javadoc 工具默认只会处理以 [public](../../../Advanced/Object_Oriented/Keyword/Access_Modifier/public.md) 或 [protected](../../../Advanced/Object_Oriented/Keyword/Access_Modifier/protected.md) 修饰的类、接口、方法、成员变量、构造器和内部类之前的文档注释**。如果要提取 [private 修饰](../../../Advanced/Object_Oriented/Keyword/Access_Modifier/private.md)的部分，需要使用 `-private`。


# Javadoc用法

## Javadoc 命令

javadoc 命令**语法格式**：

```shell
javadoc [options] [packagenames] [sourcefilenames] [-subpackages pkg1:pkg2:...] [@argfiles]
```

**说明**：

- `options`：表示 javadoc 命令选项。
- `packagenames`：表示包名。一系列包的名称，以空格分隔，如 `java.lang java.lang.reflect java.awt` 必须单独指定要记录的每个包。不允许使用通配符；使用 `-subpackages` 进行递归。Javadoc 工具用于 `-sourcepath` 查找这些包名称。
- `sourcefilenames`：表示源文件名。
- `-subpackages pkg1:pkg2:…`：从指定包中的源文件并在其子包中递归生成文档。
- `@argfiles`：一个或多个文件，其中包含以任何顺序排列的 Javadoc 选项、包名和源文件名列表。

**在 CMD (命令提示符)中查看 javadoc 的用法和选项**：

```shell
javadoc -help
```

**Javadoc 命令的常用选项**：

<img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208222154501.png" alt="图片10" style="zoom:67%;" />

## 使用 Javadoc 生成 API 文档

第一步：新建一个名为Test.txt的空白记事本，输入以下代码：

```java
/**
*@author letengzz
*@version jdk1.8.0
*/
public class Test{    
    /**     
    * 求输入两个参数范围以内整数的和     
    * @param n 接收的第一个参数，范围起点     
    * @param m 接收的第二个参数，范围终点     
    * @return 两个参数范围以内整数的和     
    */    
    public int add(int n, int m) {        
        int sum = 0;        
        for (int i = n; i <= m; i++) {            
            sum = sum + i;        
        }        
        return sum;    
    }
} 
```

第二步：将文件扩展名改为.java，即改后为`Test.java`

第三步：在`Test.java`文件所在的目录中打开 cmd 窗口，执行以下命令：

- `javadoc -author -version Test.java`：此命令没有考虑编码格式问题，注释中有汉字可能会乱码。
- `javadoc -encoding UTF-8 -charset UTF-8 Test.java`：可以解决编码问题。

输入命令后，按回车键，等待生成文件。
Test.java文件所在的目录中将会生成Test.html文档文件，打开如下图所示：

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208222154559.png)

# 文档注释的格式

在编写文档注释的过程中，有时需要添加 HTML 标签，比如：需要换行时，应该使用`<br>`，而不是一个回车符；需要分段时，应该使用`<p>`。

例如把上面 Test 类改为以下代码：

```java
package test;

/**
* @author letengzz<br>
*         哈哈哈
* @version 1.8.0<br>
*          1.9.0
*/
public class Test {
    public static void main(String[] args) {
        System.out.println("芭比Q");
    }
}
```

![image-20220822215139236](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208222154335.png)

Javadoc 并不是将代码中的文档注释直接复制到帮助文档的 HTML 文件中，而是读取每一行后，删除前面的`*`号及`*`以前的空格再输入到 HTML 文档。

```java
/**
* first line. <br>
******* second line. <br>
\* third line.
*/
```

编译输出后的 HTML 源码：

```html
first line. <br>
second line. <br>
third line.
```

注释前面的`*`号允许连续使用多个，其效果和使用一个`*`号一样，但多个`*`前不能有其他字符分隔，否则分隔符及后面的`*`号都将作为文档的内容。
