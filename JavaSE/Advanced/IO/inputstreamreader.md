# 转换流

当文件编码格式与读取格式不同时，会出现乱码问题。当存储的文字较多时，也会出现解码不正确的问题，且字节长度无法根据解码内容自动设定，此时就需要转换流来完成。

使用转换流可以在一定程度上避免乱码，还可以指定输入输出所使用的字符集。

## InputStreamReader

InputStreamReader 用于将字节输入流转换为字符输入流，是字节流转到字符流的一个桥梁。InputStreamReader是Reader的子类。

## OutputStreamWriter

OutputStreamWriter 用于将字节输出流转换为字符输出流。OutputStreamWriter是Writer的子类

## 使用方式

在 java.txt 中输出“你好”这 6 个字，将 java.txt 保存为“UTF-8”的格式，然后通过字节流的方式读取：

```Java
public static void main(String[] args) {    
    try {        
        FileInputStream fis = new FileInputStream("D://java.txt");        
        int b = 0;        
        while ((b = fis.read()) != -1) { 
            System.out.print((char) b);        
        }    
    } catch (FileNotFoundException e) {        
        // TODO Auto-generated catch block        
        e.printStackTrace();    
    } catch (IOException e) {        
        // TODO Auto-generated catch block        
        e.printStackTrace();    
    }
}
```

输出结果为 `C??????????`，我们发现中文都是乱码。下面用字节数组，并通过字符串设定编码格式来显式内容，代码如下：

```
public static void main(String[] args) {    try {        FileInputStream fis = new FileInputStream("D://java.txt");        byte b[] = new byte[1024];        int len = 0;        while ((len = fis.read(b)) != -1) {            System.out.print(new String(b, 0, len, "UTF-8"));        }    } catch (FileNotFoundException e) {        // TODO Auto-generated catch block        e.printStackTrace();    } catch (IOException e) {        // TODO Auto-generated catch block        e.printStackTrace();    }}
```

这时输出结果为 `C语言中文网`，但是当存储的文字较多时，会出现解码不正确的问题，且字节长度无法根据解码内容自动设定，此时就需要转换流来完成。代码如下：

```java
public static void main(String[] args) {    
    try {        
        FileInputStream fis = new FileInputStream("D://java.txt");        
        InputStreamReader isr = new InputStreamReader(fis, "UTF-8");        
        int b = 0;       
        while ((b = isr.read()) != -1) {            
            System.out.print((char) b);    // 输出结果为“你好”        
        }    
    } catch (FileNotFoundException e) {        
        // TODO Auto-generated catch block        
        e.printStackTrace();    
    } catch (IOException e) {        
        // TODO Auto-generated catch block        
        e.printStackTrace();    
    }
}
```

例 2

下面以获取键盘输入为例来介绍转换流的用法。Java 使用 System.in 代表标准输出，即键盘输入，但这个标准输入流是 InputStream 类的实例，使用不太方便，而且键盘输入内容都是文本内容，所以可以使用 InputStreamReader 将其转换成字符输入流，普通的 Reader 读取输入内容时依然不太方便，可以将普通的 Reader 再次包装成 BufferedReader，利用 BufferedReader 的 readLine() 方法可以一次读取一行内容。程序如下所示。

```java 
public static void main(String[] args) {    
    try {        
        // 将 System.in 对象转换成 Reader 对象        
        InputStreamReader reader = new InputStreamReader(System.in);        
        // 将普通的Reader 包装成 BufferedReader        
        BufferedReader br = new BufferedReader(reader);        
        String line = null;        
        // 利用循环方式来逐行的读取        
        while ((line = br.readLine()) != null) {            
            // 如果读取的字符串为“exit”，则程序退出            
            if (line.equals("exit")) {                
                System.exit(1);            
            }            
            // 打印读取的内容            
            System.out.println("输入内容为：" + line);        
        }    
    } catch (IOException e) {        
        // TODO Auto-generated catch block        
        e.printStackTrace();    
    }
}
```

上面代码第 4 行和第 6 行将 System.in 包装成 BufferedReader，BufferReader 流具有缓冲功能，它可以一次读取一行文本，以换行符为标志，如果它没有读到换行符，则程序堵塞，等到读到换行符为止。运行上面程序可以发现这个特征，在控制台执行输入时，只有按下回车键，程序才会打印出刚刚输入的内容。

由于 BufferedReader 具有一个 readLine() 方法，可以非常方便地进行一次读入一行内容，所以经常把读入文本内容地输入流包装成 BufferedReader，用来方便地读取输入流的文本内容。

## 为什么没有字符流转字节流的转换流

字节流比字符流的使用范围要更广，但字符流比字节流操作方便。如果有一个流已经是字符流了，也就是说，是一个用起来更方便的流，为什么要转换成字节流呢？反之，如果现在有一个字节流，但可以确定这个字节流的内容都是文本内容，那么把它转换成字符流来处理就会更方便一些，所以 Java 只提供了将字节流转换成字符流的转换流，没有提供将字符流转换成字节流的转换流。