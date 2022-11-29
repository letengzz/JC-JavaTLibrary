# 使用foreach循环遍历Collection集合

《[Java Iterator遍历Collection集合元素](http://c.biancheng.net/view/6795.html)》一节中主要讲解如何使用 Iterator 接口迭代访问 Collection 集合里的元素，除了这个方法之外，我们还可以使用 [Java](http://c.biancheng.net/java/) 5 提供的 foreach 循环迭代访问集合元素，而且更加便捷。如下程序示范了使用 foreach 循环来迭代访问集合元素。

```
public class ForeachTest {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add("C语言中文网Java教程");        objs.add("C语言中文网C语言教程");        objs.add("C语言中文网C++教程");        for (Object obj : objs) {            // 此处的obj变量也不是集合元素本身            String obj1 = (String) obj;            System.out.println(obj1);            if (obj1.equals("C语言中文网Java教程")) {                // 下面代码会引发 ConcurrentModificationException 异常                objs.remove(obj);            }        }        System.out.println(objs);    }}
```

输出结果为：

C语言中文网C++教程
C语言中文网C语言教程
C语言中文网Java教程
[C语言中文网C++教程, C语言中文网C语言教程]

上面代码使用 foreach 循环来迭代访问 Collection 集合里的元素更加简洁，这正是 JDK 1.5 的 foreach 循环带来的优势。与使用 Iterator 接口迭代访问集合元素类似的是，foreach 循环中的迭代变量也不是集合元素本身，系统只是依次把集合元素的值赋给迭代变量，因此在 foreach 循环中修改迭代变量的值也没有任何实际意义。

同样，当使用 foreach 循环迭代访问集合元素时，该集合也不能被改变，否则将引发 ConcurrentModificationException 异常。所以上面程序中第 14 行代码处将引发该异常。