# Java 7新特性：多异常捕获

多 catch 代码块虽然客观上提高了程序的健壮性，但是也导致了程序代码量大大增加。

有些异常种类不同，但捕获之后的处理是相同的：

```java
try{
    // 可能会发生异常的语句
} catch (FileNotFoundException e) {
    // 调用方法methodA处理
} catch (IOException e) {
    // 调用方法methodA处理
} catch (ParseException e) {
    // 调用方法methodA处理
}
```

3 个不同类型的异常，要求捕获之后的处理都是调用 methodA 方法。为了解决这种问题，Java 7 推出了**多异常捕获**技术，可以把这些异常合并处理。

修改如下：

```java
try{
    // 可能会发生异常的语句
} catch (IOException | ParseException e) {
    // 调用方法methodA处理
}
```

**注意**：由于 `FileNotFoundException` 属于 `IOException` 异常，`IOException` 异常可以捕获它的所有子类异常。所以不能写成 `FileNotFoundException | IOException | ParseException` 。

使用一个 `catch` 块捕获多种类型的异常时需要**注意**如下两个地方：

- 捕获多种类型的异常时，多种异常类型之间用竖线`|`隔开。
- 捕获多种类型的异常时，异常变量有隐式的 `final` 修饰，因此程序不能对异常变量重新赋值。

**例**：

```java
public class ExceptionTest {
    public static void main(String[] args) {
        try {
            int a = Integer.parseInt(args[0]);
            int b = Integer.parseInt(args[1]);
            int c = a / b;
            System.out.println("您输入的两个数相除的结果是：" + c);
        } catch (IndexOutOfBoundsException | NumberFormatException | ArithmeticException e) {
            System.out.println("程序发生了数组越界、数字格式异常、算术异常之一");
            // 捕获多异常时，异常变量默认有final修饰
            // 所以下面代码有错
            e = new ArithmeticException("test");
        } catch (Exception e) {
            System.out.println("未知异常");
            // 捕获一种类型的异常时，异常变量没有final修饰
            // 所以下面代码完全正确
            e = new RuntimeException("test");
        }
    }
}
```

使用`IndexOutOfBoundsException|NumberFormatException|ArithmeticException`来定义异常类型，这就表明该 `catch` 块可以同时捕获这 3 种类型的异常。捕获多种类型的异常时，异常变量使用隐式的 `final` 修饰，因此上面程序的第 12 行代码将产生编译错误；捕获一种类型的异常时，异常变量没有 `final` 修饰，因此上面程序的第 17 行代码完全正确。

