# 序列化与反序列化

**序列化**：用ObjectOutputStream类保存基本类型或对象的机制。

**反序列化**：用ObjectInputStream类读取基本类型数据或对象的机制。

------

## 序列化

**序列化是指把一个Java对象变成二进制内容**。

当序列化后可以把`byte[]`保存到文件中，或者把`byte[]`通过网络传输到远程，这样，就相当于把Java对象存储到文件或者通过网络传输出去了。

**把一个Java对象序列化**：

一个Java对象要能序列化，必须实现一个特殊的`java.io.Serializable`接口

**Serializable的定义**：

```Java
public interface Serializable {
}
```

`Serializable`接口没有定义任何方法，它是一个空接口。我们把这样的空接口称为"标记接口"(`Marker Interface`)，实现了标记接口的类仅仅是给自身贴了个“标记”，并没有增加任何方法。

**例**：

1. 把一个Java对象变为`byte[]`数组，需要使用`ObjectOutputStream`。它负责把一个Java对象写入一个字节流：

   ```Java
   import java.io.*;
   import java.util.Arrays;
   public class Main {
       public static void main(String[] args) throws IOException {
           ByteArrayOutputStream buffer = new ByteArrayOutputStream();
           try (ObjectOutputStream output = new ObjectOutputStream(buffer)) {
               // 写入int:
               output.writeInt(12345);
               // 写入String:
               output.writeUTF("Hello");
               // 写入Object:
               output.writeObject(Double.valueOf(123.456));
           }
           System.out.println(Arrays.toString(buffer.toByteArray()));
       }
   }
   ```

   `ObjectOutputStream`既可以写入基本类型，如`int`，`boolean`，也可以写入`String`（以UTF-8编码），还可以写入实现了`Serializable`接口的`Object`。因为写入`Object`时需要大量的类型信息，所以写入的内容很大。

2. 把一个Java对象变为文件：

   > Javabeen/Student.java

   ```java 
   import java.io.Serializable;
   import java.util.Objects;
   
   public class Student implements Serializable {
       private int id;
       private String name;
       //版本号
       private static final long serialVersionUID = 1L;
   
       private int a;
   
       public Student(int id, String name) {
           this.id = id;
           this.name = name;
       }
   
       public Student() {
       }
   
       public int getId() {
           return id;
       }
   
       public void setId(int id) {
           this.id = id;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       @Override
       public String toString() {
           return "Student{" +
                   "id=" + id +
                   ", name='" + name + '\'' +
                   '}';
       }
   
       @Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (o == null || getClass() != o.getClass()) return false;
           Student student = (Student) o;
           return id == student.id && Objects.equals(name, student.name);
       }
   
       @Override
       public int hashCode() {
           return Objects.hash(id, name);
       }
   }
   ```

   > Main.java

   ```java 
   public class Main(){
       public static void main(String[] args){
           ObjectOutputStream oos = null;
           try{
               oos = new ObjectOutputStream(new FileOutputStream("D:1.txt"));
               Student stu = new Student(1,"kunkun");
               oos.writeObject(stu);
           }catch(Exception e){
               e.printStackTrace();
           }finally{
               try{
                   oos.close();
               }catch(Exception e){
                   e.printStackTrace();
               }
           }
       }
   }
   ```

## 反序列化

有序列化，就有反序列化，即**把一个二进制内容(也就是`byte[]`数组)变回Java对象**。有了反序列化，保存到文件中的`byte[]`数组又可以“变回”Java对象，或者从网络上读取`byte[]`并把它“变回”Java对象。

和`ObjectOutputStream`相反，`ObjectInputStream`负责从一个字节流读取Java对象：

```Java
try (ObjectInputStream input = new ObjectInputStream(...)) {
    int n = input.readInt();
    String s = input.readUTF();
    Double d = (Double) input.readObject();
}
```

除了能读取基本类型和`String`类型外，调用`readObject()`可以直接返回一个`Object`对象。要把它变成一个特定类型，必须强制转型。

`readObject()`可能抛出的异常：

- `ClassNotFoundException`：没有找到对应的Class；
- `InvalidClassException`：Class不匹配。

对于`ClassNotFoundException`，这种情况常见于一台电脑上的Java程序把一个Java对象，例如，`Person`对象序列化以后，通过网络传给另一台电脑上的另一个Java程序，但是这台电脑的Java程序并没有定义`Person`类，所以无法反序列化。

对于`InvalidClassException`，这种情况常见于序列化的`Person`对象定义了一个`int`类型的`age`字段，但是反序列化时，`Person`类定义的`age`字段被改成了`long`类型，所以导致class不兼容。

为了避免这种class定义变动导致的不兼容，Java的序列化允许class定义一个特殊的[`serialVersionUID`](serialVersionUID.md)静态变量，用于标识Java类的序列化"版本"，通常可以由IDE自动生成。如果增加或修改了字段，可以改变`serialVersionUID`的值，这样就能自动阻止不匹配的class版本：

```java 
public class Person implements Serializable {
    private static final long serialVersionUID = 2709425275741743919L;
}
```

**注意**：

反序列化时，由JVM直接构造出Java对象，不调用构造方法，构造方法内部的代码，在反序列化时根本不可能执行。

## 安全性

因为Java的序列化机制可以导致一个实例能直接从`byte[]`数组创建，而不经过构造方法，因此，它存在一定的安全隐患。一个精心构造的`byte[]`数组被反序列化后可以执行特定的Java代码，从而导致严重的安全漏洞。

实际上，Java本身提供的基于对象的序列化和反序列化机制既存在安全性问题，也存在兼容性问题。更好的序列化方法是通过JSON这样的通用数据结构来实现，只输出基本类型(包括String)的内容，而不存储任何与代码相关的信息。

## 总结

- 可序列化的Java对象必须实现`java.io.Serializable`接口，类似`Serializable`这样的空接口被称为“标记接口”(`Marker Interface`)

- 反序列化时不调用构造方法，可设置`serialVersionUID`作为版本号（非必需）；

- Java的序列化机制仅适用于Java，如果需要与其它语言交换数据，必须使用通用的序列化方法，例如JSON。