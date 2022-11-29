# 使用`sort()`对数组排序

Java 语言使用 Arrays 类提供的 `sort()` 方法来对数组进行排序。

## 升序

使用 `java.util.Arrays` 类中的 `sort()` 方法对数组进行升序分为以下两步：

1. 导入 `java.util.Arrays` 包。
2. 使用 `Arrays.sort`(数组名)语法对数组进行排序，排序规则是从小到大，即升序。

**例**：

假设在数组 scores 中存放了 5 名学生的成绩，现在要实现从低到高排列的功能。使用 `Arrays.sort()` 方法来实现：

```java
public static void main(String[] args) {    
    // 定义含有5个元素的数组    
    double[] scores = new double[] { 78, 45, 85, 97, 87 };    
    System.out.println("排序前数组内容如下：");    
    // 对scores数组进行循环遍历    
    for (int i = 0; i < scores.length; i++) {        
        System.out.print(scores[i] + "\t");    
    }    
    System.out.println("\n排序后的数组内容如下：");    
    // 对数组进行排序    
    Arrays.sort(scores);    
    // 遍历排序后的数组    
    for (int j = 0; j < scores.length; j++) {        
        System.out.print(scores[j] + "\t");    
    }
}
```

要对一个数组进行升序排列，只需要调用 `Arrays.sort()` 方法即可。

运行结果：

> 排序前数组内容如下：
> 78.0    45.0    85.0    97.0    87.0   
> 排序后的数组内容如下：
> 45.0    78.0    85.0    87.0    97.0

## 降序

利用 `Collections.reverseOrder()` 方法：

```java
public static void main(String[] args) {    
    Integer[] a = { 9, 8, 7, 2, 3, 4, 1, 0, 6, 5 };    
    // 数组类型为Integer    
    Arrays.sort(a, Collections.reverseOrder());    
    for (int arr : a) {        
        System.out.print(arr + " ");    
    }
}
```

运行结果：

> 9 8 7 6 5 4 3 2 1 0 

实现 Comparator 接口的复写 `compare()` 方法，代码如下:

```java 
public class Test {    
    public static void main(String[] args) {        
        /*         
        * 注意，要想改变默认的排列顺序，不能使用基本类型（int,double,char）而要使用它们对应的类         
        */        
        Integer[] a = { 9, 8, 7, 2, 3, 4, 1, 0, 6, 5 };        
        // 定义一个自定义类MyComparator的对象        
        Comparator cmp = new MyComparator();        
        Arrays.sort(a, cmp);        
        for (int arr : a) {            
            System.out.print(arr + " ");        
        }    
    }
}
// 实现Comparator接口
class MyComparator implements Comparator<Integer> {    
    @Override    
    public int compare(Integer o1, Integer o2) {        
        /*         
        * 如果o1小于o2，我们就返回正值，如果o1大于o2我们就返回负值， 这样颠倒一下，就可以实现降序排序了,反之即可自定义升序排序了      */        
        return o2 - o1;    
    }
}
```

输出结果如下所示。

> 9 8 7 6 5 4 3 2 1 0 

**注意**：使用以上两种方法时，数组必须是包装类型，否则会编译不通过。

在 Java 中实现数组排序的方式很多，除了利用以上的几种方法外，还可以编写自定义方法来实现自己的排序算法。