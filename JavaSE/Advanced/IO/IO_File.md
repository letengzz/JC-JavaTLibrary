# Java File类(文件操作类)

在计算机系统中，文件是非常重要的存储方式。Java的标准库`java.io`提供了`File`对象来操作文件和目录。

File 类是 java.io 包中唯一代表磁盘文件本身的对象，也就是说，如果希望在程序中操作文件和目录，则都可以通过 File 类来完成。File 类定义了一些方法来操作文件，如新建、删除、重命名文件和目录等。

File 类不能访问文件内容本身，如果需要访问文件内容本身，则需要使用输入/输出流。

**构造方法**：

1. `File(String path)`：如果 path 是实际存在的路径，则该 File 对象表示的是目录；如果 path 是文件名，则该 File 对象表示的是文件。
2. `File(String path, String name)`：path 是路径名，name 是文件名。
3. `File(File dir, String name)`：dir 是路径对象，name 是文件名。
4. `File(URI uri)`：通过将给定的URI转换为抽象路径名来创建一个新的File实例。

**注意**：构造一个`File`对象，即使传入的文件或目录不存在，代码也不会出错，因为构造一个`File`对象，并不会导致任何磁盘操作。只有当我们调用`File`对象的某些方法的时候，才真正进行磁盘操作。

```Java
//构造方法:File(String path)
File f1 = new File("D:\\1.txt");
File f2 = new File("D:/2.txt");

//构造方法:File(String path, String name)
File f3 = new File("D:\\demo\\","3.txt");

//构造方法:File(File dir, String name)
File f4 = new File("D:\\demo");
File f5 = new File(f4,"3.txt");

//构造方法:File(URI uri)
File File6 = new File(new URI("file:///c:/a.bat"));
```

**File 类的常用方法**：

![](D:\Data\typora\photo\图片35.png)

**File 类中常量**：

- `public static final String pathSeparator`：指的是分隔连续多个路径字符串的分隔符，表示方式为字符串形式。

  Windows 下指`;`。例如 `java -cp test.jar;abc.jar HelloWorld`。

- `public static final char pathSeparatorChar`：同pathSeparator，但是表示方式为char类型。

- `public static final String separator`：用来分隔同一个路径字符串中的目录的，表示方式为字符串形式。

  Windows 下指`/`。例如 `C:/Program Files/Common Files`。

- `public static final char separatorChar`：同separator，但表示方式为char类型。

**注意**：File 类的常量定义的命名规则不符合标准命名规则，常量名没有全部大写，这是因为 Java 的发展经过了一段相当长的时间，而命名规范也是逐步形成的，File 类出现较早，所以当时并没有对命名规范有严格的要求，这些都属于 Java 的历史遗留问题。

------

**路径**：

构造File对象时，既可以传入绝对路径，也可以传入相对路径。

绝对路径是以根目录开头的完整路径：

```Java
File f = new File("C:\\Windows\\notepad.exe");
```

**注意**：Windows平台使用`\`作为路径分隔符，在Java字符串中需要用`\\`([转义字符](../../../Appendix/ESC/README.md))表示一个`\`。Linux平台使用`/`作为路径分隔符：

```Java
File f = new File("/usr/bin/javac");
```

传入相对路径时，相对路径前面加上当前目录就是绝对路径：

```java
// 假设当前目录是C:\Docs
File f1 = new File("sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File(".\\sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File("..\\sub\\javac"); // 绝对路径是C:\sub\javac
```

说明：**可以用`.`表示当前目录，`..`表示上级目录**。

> Windows 的路径分隔符使用反斜线“\”，而 Java 程序中的反斜线表示转义字符，所以如果需要在 Windows 的路径下包括反斜线，则应该使用两条反斜线或直接使用斜线“/”也可以。Java 程序支持将斜线当成平台无关的路径分隔符。

假设在 Windows 操作系统中有一文件 `D:\javaspace\hello.java`，在 Java 中使用的时候，其路径的写法应该为 `D:/javaspace/hello.java` 或者 `D:\\javaspace\\hello.java`。

File对象有3种形式表示的路径：

- `getPath()`：返回构造方法传入的路径
- `getAbsolutePath()`：返回绝对路径
- `getCanonicalPath`：它和绝对路径类似，但是返回的是规范路径

```java
import java.io.*;
public class Main {
    public static void main(String[] args) throws IOException {
        File f = new File("..");
        System.out.println(f.getPath());
        System.out.println(f.getAbsolutePath());
        System.out.println(f.getCanonicalPath());
    }
}
```

绝对路径可以表示成`C:\Windows\System32\..\notepad.exe`

规范路径就是把`.`和`..`转换成标准的绝对路径后的路径：`C:\Windows\notepad.exe`。

因为Windows和Linux的路径分隔符不同，File对象有一个静态变量用于表示当前平台的系统分隔符：

```java
System.out.println(File.separator); // 根据当前平台打印"\"或"/"
```

## 文件和目录

`File`对象既可以表示文件，也可以表示目录。

**注意**：构造一个`File`对象，即使传入的文件或目录不存在，代码也不会出错，因为构造一个`File`对象，并不会导致任何磁盘操作。只有当我们调用`File`对象的某些方法的时候，才真正进行磁盘操作。

用`File`对象获取到一个文件时，还可以进一步判断文件的权限和大小：

- `boolean canRead()`：是否可读
- `boolean canWrite()`：是否可写
- `boolean canExecute()`：是否可执行
- `long length()`：文件字节大小

对目录而言，是否可执行表示能否列出它包含的文件和子目录。

例如，调用`isFile()`，判断该`File`对象是否是一个已存在的文件，调用`isDirectory()`，判断该`File`对象是否是一个已存在的目录：

```java
import java.io.*;
public class Main {
    public static void main(String[] args) throws IOException {
        File f1 = new File("C:\\Windows");
        File f2 = new File("C:\\Windows\\notepad.exe");
        File f3 = new File("C:\\Windows\\nothing");
        System.out.println(f1.isFile());
        System.out.println(f1.isDirectory());
        System.out.println(f2.isFile());
        System.out.println(f2.isDirectory());
        System.out.println(f3.isFile());
        System.out.println(f3.isDirectory());
    }
}
```



## 获取文件属性

在 Java 中获取文件属性信息的第一步是先创建一个 File 类对象并指向一个已存在的文件， 然后调用表 1 中的方法进行操作。

例

假设有一个文件位于 `C:\windows\notepad.exe`。编写 Java 程序获取并显示该文件的长度、是否可写、最后修改日期以及文件路径等属性信息。实现代码如下：

```
public class Test02 {    public static void main(String[] args) {        String path = "C:/windows/"; // 指定文件所在的目录        File f = new File(path, "notepad.exe"); // 建立File变量,并设定由f变量引用        System.out.println("C:\\windows\\notepad.exe文件信息如下：");        System.out.println("============================================");        System.out.println("文件长度：" + f.length() + "字节");        System.out.println("文件或者目录：" + (f.isFile() ? "是文件" : "不是文件"));        System.out.println("文件或者目录：" + (f.isDirectory() ? "是目录" : "不是目录"));        System.out.println("是否可读：" + (f.canRead() ? "可读取" : "不可读取"));        System.out.println("是否可写：" + (f.canWrite() ? "可写入" : "不可写入"));        System.out.println("是否隐藏：" + (f.isHidden() ? "是隐藏文件" : "不是隐藏文件"));        System.out.println("最后修改日期：" + new Date(f.lastModified()));        System.out.println("文件名称：" + f.getName());        System.out.println("文件路径：" + f.getPath());        System.out.println("绝对路径：" + f.getAbsolutePath());    }}
```

在上述代码中 File 类构造方法的第一个参数指定文件所在位置，这里使用`C:/`作为文件的实际路径；第二个参数指定文件名称。创建的 File 类对象为 f，然后通过 f 调用方法获取相应的属性，最终运行效果如下所示。

```
C:\windows\notepad.exe文件信息如下：
============================================
文件长度：193536字节
文件或者目录：是文件
文件或者目录：不是目录
是否可读：可读取
是否可写：可写入
是否隐藏：不是隐藏文件
最后修改日期：Mon Dec 28 02:55:19 CST 2016
文件名称：notepad.exe
文件路径：C:\windows\notepad.exe
绝对路径：C:\windows\notepad.exe
```

## 创建和删除文件

当File对象表示一个文件时，可以通过`createNewFile()`创建一个新文件，用`delete()`删除该文件：

```
File file = new File("/path/to/file");
if (file.createNewFile()) {
    // 文件创建成功:
    // TODO:
    if (file.delete()) {
        // 删除文件成功:
    }
}
```

有些时候，程序需要读写一些临时文件，File对象提供了`createTempFile()`来创建一个临时文件，以及`deleteOnExit()`在JVM退出时自动删除该文件。

```
import java.io.*;
```

 Run

File 类不仅可以获取已知文件的属性信息，还可以在指定路径创建文件，以及删除一个文件。创建文件需要调用 createNewFile() 方法，删除文件需要调用 delete() 方法。无论是创建还是删除文件通常都先调用 exists() 方法判断文件是否存在。

例 2

假设要在 C 盘上创建一个 test.txt 文件，程序启动时会检测该文件是否存在，如果不存在则创建；如果存在则删除它再创建。

实现代码如下：

```
public class Test03 {    public static void main(String[] args) throws IOException {        File f = new File("C:\\test.txt"); // 创建指向文件的File对象        if (f.exists()) // 判断文件是否存在        {            f.delete(); // 存在则先删除        }        f.createNewFile(); // 再创建    }}
```

运行程序之后可以发现，在 C 盘中已经创建好了 test.txt 文件。但是如果在不同的操作系统中，路径的分隔符是不一样的，例如：

- Windows 中使用反斜杠`\`表示目录的分隔符。
- Linux 中使用正斜杠`/`表示目录的分隔符。


那么既然 Java 程序本身具有可移植性的特点，则在编写路径时最好可以根据程序所在的操作系统自动使用符合本地操作系统要求的分隔符，这样才能达到可移植性的目的。要实现这样的功能，则就需要使用 File 类中提供的两个常量。

代码修改如下：

```
public static void main(String[] args) throws IOException {    String path = "C:" + File.separator + "test.txt"; // 拼凑出可以适应操作系统的路径    File f = new File(path);    if (f.exists()) // 判断文件是否存在    {        f.delete(); // 存在则先删除    }    f.createNewFile(); // 再创建}
```

程序的运行结果和前面程序一样，但是此时的程序可以在任意的操作系统中使用。

注意：在操作文件时一定要使用 File.separator 表示分隔符。在程序的开发中，往往会使用 Windows 开发环境，因为在 Windows 操作系统中支持的开发工具较多，使用方便，而在程序发布时往往是直接在 Linux 或其它操作系统上部署，所以这时如果不使用 File.separator，则程序运行就有可能存在问题。关于这一点我们在以后的开发中一定要有所警惕。

## 创建和删除目录

File 类除了对文件的创建和删除外，还可以创建和删除目录。创建目录需要调用 mkdir() 方法，删除目录需要调用 delete() 方法。无论是创建还是删除目录都可以调用 exists() 方法判断目录是否存在。

例 3

编写一个程序判断 C 盘根目录下是否存在 config 目录，如果存在则先删除再创建。实现代码如下：

```
public class Test04 {    public static void main(String[] args) {        String path = "C:/config/"; // 指定目录位置        File f = new File(path); // 创建File对象        if (f.exists()) {            f.delete();        }        f.mkdir(); // 创建目录    }}
```

## 遍历目录

当File对象表示一个目录时，可以使用`list()`和`listFiles()`列出目录下的文件和子目录名。`listFiles()`提供了一系列重载方法，可以过滤不想要的文件和目录：

```
import java.io.*;
```

 Run

和文件操作类似，File对象如果表示一个目录，可以通过以下方法创建和删除目录：

- `boolean mkdir()`：创建当前File对象表示的目录；
- `boolean mkdirs()`：创建当前File对象表示的目录，并在必要时将不存在的父目录也创建出来；
- `boolean delete()`：删除当前File对象表示的目录，当前目录必须为空才能删除成功。

通过遍历目录可以在指定的目录中查找文件，或者显示所有的文件列表。File 类的 list() 方法提供了遍历目录功能，该方法有如下两种重载形式。

###  String[] list()

该方法表示返回由 File 对象表示目录中所有文件和子目录名称组成的字符串数组，如果调用的 File 对象不是目录，则返回 null。

提示：list() 方法返回的数组中仅包含文件名称，而不包含路径。但不保证所得数组中的相同字符串将以特定顺序出现，特别是不保证它们按字母顺序出现。

### String[] list(FilenameFilter filter)

该方法的作用与 list() 方法相同，不同的是返回数组中仅包含符合 filter 过滤器的文件和目录，如果 filter 为 null，则接受所有名称。

例 4

假设要遍历 C 盘根目录下的所有文件和目录，并显示文件或目录名称、类型及大小。使用 list() 方法的实现代码如下：

```
public class Test05 {    public static void main(String[] args) {        File f = new File("C:/"); // 建立File变量,并设定由f变量变数引用        System.out.println("文件名称\t\t文件类型\t\t文件大小");        System.out.println("===================================================");        String fileList[] = f.list(); // 调用不带参数的list()方法        for (int i = 0; i < fileList.length; i++) { // 遍历返回的字符数组            System.out.print(fileList[i] + "\t\t");            System.out.print((new File("C:/", fileList[i])).isFile() ? "文件" + "\t\t" : "文件夹" + "\t\t");            System.out.println((new File("C:/", fileList[i])).length() + "字节");        }    }}
```


由于 list() 方法返回的字符数组中仅包含文件名称，因此为了获取文件类型和大小，必须先转换为 File 对象再调用其方法。如下所示的是实例的运行效果：

```
文件名称  文件类型  文件大小
===================================================
$Recycle.Bin  文件夹  4096字节
Documents and Settings  文件夹  0字节
Download  文件夹  0字节
DRIVERS  文件夹  0字节
FibocomLog  文件夹  0字节
Gateface  文件夹  0字节
GFPageCache  文件夹  0字节
hiberfil.sys  文件  3375026176字节
Intel  文件夹  0字节
KuGou  文件夹  0字节
logs  文件夹  0字节
msdia80.dll  文件  904704字节
MSOCache  文件夹  0字节
MyDownloads  文件夹  0字节
MyDrivers  文件夹  0字节
news.template  文件  417字节
NVIDIA  文件夹  0字节
OneDriveTemp  文件夹  0字节
opt  文件夹  0字节
pagefile.sys  文件  6442450944字节
PerfLogs  文件夹  0字节
Program Files  文件夹  12288字节
Program Files (x86)  文件夹  8192字节
ProgramData  文件夹  12288字节
QMDownload  文件夹  0字节
Recovery  文件夹  0字节
swapfile.sys  文件  268435456字节
System Volume Information  文件夹  12288字节
Users  文件夹  4096字节
Windows  文件夹  16384字节
```

例 5

假设希望只列出目录下的某些文件，这就需要调用带过滤器参数的 list() 方法。首先需要创建文件过滤器，该过滤器必须实现 `java.io.FilenameFilter` 接口，并在 accept() 方法中指定允许的文件类型。

如下所示为允许 SYS、TXT 和 BAK 格式文件的过滤器实现代码：

```
public class ImageFilter implements FilenameFilter {    // 实现 FilenameFilter 接口    @Override    public boolean accept(File dir, String name) {        // 指定允许的文件类型        return name.endsWith(".sys") || name.endsWith(".txt") || name.endsWith(".bak");    }}
```

上述代码创建的过滤器名称为 ImageFilter，接下来只需要将该名称传递给 list() 方法即可实现筛选文件。如下所示为修改后的 list() 方法，其他代码与例 4 相同，这里不再重复。

String fileList[] = f.list(new ImageFilter());


再次运行程序，遍历结果如下所示：

```
文件名称        文件类型        文件大小
===================================================
offline_FtnInfo.txt        文件        296字节
pagefile.sys        文件        8436592640字节
```

### Path

Java标准库还提供了一个`Path`对象，它位于`java.nio.file`包。`Path`对象和`File`对象类似，但操作更加简单：

```
import java.io.*;
import java.nio.file.*;
```

 Run

如果需要对目录进行复杂的拼接、遍历等操作，使用`Path`对象更方便。

