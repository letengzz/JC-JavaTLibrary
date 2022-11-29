# 抑制编译器警告：`@SuppressWarnings`

Java 中的 `@SuppressWarnings` 注解指示被该注解修饰的程序元素(以及该程序元素中的所有子元素)取消显示指定的编译器警告，且会一直作用于该程序元素的所有子元素。例如，使用 `@SuppressWarnings` 修饰某个类取消显示某个编译器警告，同时又修饰该类里的某个方法取消显示另一个编译器警告，那么该方法将会同时取消显示这两个编译器警告。

`@SuppressWarnings` 注解主要用在取消一些编译器产生的警告对代码左侧行列的遮挡，有时候这样会挡住我们断点调试时打的断点：

![image-20220815164731093](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208151701931.png)


如果你确认程序中的警告没有问题，可以不用理会。通常情况下，如果程序中使用没有泛型限制的集合将会引起编译器警告，为了避免这种编译器警告，可以使用 `@SuppressWarnings` 注解消除这些警告。

注解的使用有以下三种：

1. **抑制单类型的警告**：`@SuppressWarnings("unchecked")`
2. **抑制多类型的警告**：`@SuppressWarnings("unchecked","rawtypes")`
3. **抑制所有类型的警告**：`@SuppressWarnings("unchecked")`

**抑制警告的关键字**：

![图片8](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208151718641.png)

**例**：

```java
public class HelloWorld {
    @SuppressWarnings({ "deprecation" })
    public static void main(String[] args) {
        Person p = new Person();
        p.setNameAndAge("小明", 20);
        p.name = "小明";
    }
}
```

在 IDE中显示：

![image-20220815171722271](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208151719702.png)

![image-20220815171340326](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208151719112.png)


使用 `@SuppressWarnings({ "deprecation" })` 注解了 main 方法。在使用`@Deprecated`注解的 Person 代码中，这些 API 已经过时了，所以代码第 4 行~第 6 行是编译警告，但是在使用了 `@SuppressWarnings` 注解之后会发现程序代码的警告没有了。