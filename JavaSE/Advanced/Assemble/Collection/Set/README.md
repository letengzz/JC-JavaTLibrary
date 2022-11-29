# Set集合

# HashSet类

# TreeSet类

Set 集合类似于一个罐子，程序可以依次把多个对象“丢进”Set 集合，而 Set 集合通常不能记住元素的添加顺序。也就是说 Set 集合中的对象不按特定的方式排序，只是简单地把对象加入集合。Set 集合中不能包含重复的对象，并且最多只允许包含一个 null 元素。

Set 实现了 Collection 接口，它主要有两个常用的实现类：HashSet 类和 TreeSet类。

## HashSet 类

HashSet 是 Set 接口的典型实现，大多数时候使用 Set 集合时就是使用这个实现类。HashSet 是按照 Hash 算法来存储集合中的元素。因此具有很好的存取和查找性能。

HashSet 具有以下特点：

- 不能保证元素的排列顺序，顺序可能与添加顺序不同，顺序也有可能发生变化。
- HashSet 不是同步的，如果多个线程同时访问或修改一个 HashSet，则必须通过代码来保证其同步。
- 集合元素值可以是 null。


当向 HashSet 集合中存入一个元素时，HashSet 会调用该对象的 hashCode() 方法来得到该对象的 hashCode 值，然后根据该 hashCode 值决定该对象在 HashSet 中的存储位置。如果有两个元素通过 equals() 方法比较返回的结果为 true，但它们的 hashCode 不相等，HashSet 将会把它们存储在不同的位置，依然可以添加成功。

也就是说，两个对象的 hashCode 值相等且通过 equals() 方法比较返回结果为 true，则 HashSet 集合认为两个元素相等。

在 HashSet 类中实现了 Collection 接口中的所有方法。HashSet 类的常用构造方法重载形式如下。

- HashSet()：构造一个新的空的 Set 集合。
- HashSet(Collection<? extends E>c)：构造一个包含指定 Collection 集合元素的新 Set 集合。其中，“< >”中的 extends 表示 HashSet 的父类，即指明该 Set 集合中存放的集合元素类型。c 表示其中的元素将被存放在此 Set 集合中。


下面的代码演示了创建两种不同形式的 HashSet 对象。

```
HashSet hs = new HashSet();    // 调用无参的构造函数创建HashSet对象HashSet<String> hss = new HashSet<String>();    // 创建泛型的 HashSet 集合对象
```

#### 例 1

编写一个 [Java](http://c.biancheng.net/java/) 程序，使用 HashSet 创建一个 Set 集合，并向该集合中添加 4 套教程。具体实现代码如下：

```
public static void main(String[] args) {    HashSet<String> courseSet = new HashSet<String>(); // 创建一个空的 Set 集合    String course1 = new String("Java入门教程");    String course2 = new String("Python基础教程");    String course3 = new String("C语言学习教程");    String course4 = new String("Golang入门教程");    courseSet.add(course1); // 将 course1 存储到 Set 集合中    courseSet.add(course2); // 将 course2 存储到 Set 集合中    courseSet.add(course3); // 将 course3 存储到 Set 集合中    courseSet.add(course4); // 将 course4 存储到 Set 集合中    System.out.println("C语言中文网教程有：");    Iterator<String> it = courseSet.iterator();    while (it.hasNext()) {        System.out.println("《" + (String) it.next() + "》"); // 输出 Set 集合中的元素    }    System.out.println("有" + courseSet.size() + "套精彩教程！");}
```

如上述代码，首先使用 HashSet 类的构造方法创建了一个 Set 集合，接着创建了 4 个 String 类型的对象，并将这些对象存储到 Set 集合中。使用 HashSet 类中的 iterator() 方法获取一个 Iterator 对象，并调用其 hasNext() 方法遍历集合元素，再将使用 next() 方法读取的元素强制转换为 String 类型。最后调用 HashSet 类中的 size() 方法获取集合元素个数。

运行该程序，输出的结果如下：

```
C语言中文网教程有：
《Java入门教程》
《C语言学习教程》
《Python基础教程》
《Golang入门教程》
有4套精彩教程！
```

注意：在以上示例中，如果再向 CourseSet 集合中再添加一个名称为“Java入门教程”的 String 对象，则输出的结果与上述执行结果相同。也就是说，如果向 Set 集合中添加两个相同的元素，则后添加的会覆盖前面添加的元素，即在 Set 集合中不会出现相同的元素。

## TreeSet 类

TreeSet 类同时实现了 Set 接口和 SortedSet 接口。SortedSet 接口是 Set 接口的子接口，可以实现对集合进行自然排序，因此使用 TreeSet 类实现的 Set 接口默认情况下是自然排序的，这里的自然排序指的是升序排序。

TreeSet 只能对实现了 Comparable 接口的类对象进行排序，因为 Comparable 接口中有一个 compareTo(Object o) 方法用于比较两个对象的大小。例如 a.compareTo(b)，如果 a 和 b 相等，则该方法返回 0；如果 a 大于 b，则该方法返回大于 0 的值；如果 a 小于 b，则该方法返回小于 0 的值。

表 1 列举了 JDK 类库中实现 Comparable 接口的类，以及这些类对象的比较方式。



| 类                                                           | 比较方式                                  |
| ------------------------------------------------------------ | ----------------------------------------- |
| 包装类（BigDecimal、Biglnteger、 Byte、Double、 Float、Integer、Long 及 Short) | 按数字大小比较                            |
| Character                                                    | 按字符的 Unicode 值的数字大小比较         |
| String                                                       | 按字符串中字符的 Unicode 值的数字大小比较 |


TreeSet 类除了实现 Collection 接口的所有方法之外，还提供了如表 2 所示的方法。



| 方法名称                                       | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| E first()                                      | 返回此集合中的第一个元素。其中，E 表示集合中元素的数据类型   |
| E last()                                       | 返回此集合中的最后一个元素                                   |
| E poolFirst()                                  | 获取并移除此集合中的第一个元素                               |
| E poolLast()                                   | 获取并移除此集合中的最后一个元素                             |
| SortedSet<E> subSet(E fromElement,E toElement) | 返回一个新的集合，新集合包含原集合中 fromElement 对象与 toElement 对象之间的所有对象。包含 fromElement 对象，不包含 toElement 对象 |
| SortedSet<E> headSet<E toElement〉             | 返回一个新的集合，新集合包含原集合中 toElement 对象之前的所有对象。 不包含 toElement 对象 |
| SortedSet<E> tailSet(E fromElement)            | 返回一个新的集合，新集合包含原集合中 fromElement 对象之后的所有对 象。包含 fromElement 对象 |

注意：表面上看起来这些方法很多，其实很简单。因为 TreeSet 中的元素是有序的，所以增加了访问第一个、前一个、后一个、最后一个元素的方法，并提供了 3 个从 TreeSet 中截取子 TreeSet 的方法。

#### 例 2

本次有 5 名学生参加考试，当老师录入每名学生的成绩后，程序将按照从低到高的排列顺序显示学生成绩。此外，老师可以查询本次考试是否有满分的学生存在，不及格的成绩有哪些，90 分以上成绩的学生有几名。

下面使用 TreeSet 类来创建 Set 集合，完成学生成绩查询功能。具体的代码如下：

```
public class Test08 {    public static void main(String[] args) {        TreeSet<Double> scores = new TreeSet<Double>(); // 创建 TreeSet 集合        Scanner input = new Scanner(System.in);        System.out.println("------------学生成绩管理系统-------------");        for (int i = 0; i < 5; i++) {            System.out.println("第" + (i + 1) + "个学生成绩：");            double score = input.nextDouble();            // 将学生成绩转换为Double类型，添加到TreeSet集合中            scores.add(Double.valueOf(score));        }        Iterator<Double> it = scores.iterator(); // 创建 Iterator 对象        System.out.println("学生成绩从低到高的排序为：");        while (it.hasNext()) {            System.out.print(it.next() + "\t");        }        System.out.println("\n请输入要查询的成绩：");        double searchScore = input.nextDouble();        if (scores.contains(searchScore)) {            System.out.println("成绩为： " + searchScore + " 的学生存在！");        } else {            System.out.println("成绩为： " + searchScore + " 的学生不存在！");        }        // 查询不及格的学生成绩        SortedSet<Double> score1 = scores.headSet(60.0);        System.out.println("\n不及格的成绩有：");        for (int i = 0; i < score1.toArray().length; i++) {            System.out.print(score1.toArray()[i] + "\t");        }        // 查询90分以上的学生成绩        SortedSet<Double> score2 = scores.tailSet(90.0);        System.out.println("\n90 分以上的成绩有：");        for (int i = 0; i < score2.toArray().length; i++) {            System.out.print(score2.toArray()[i] + "\t");        }    }}
```

如上述代码，首先创建一个 TreeSet 集合对象 scores，并向该集合中添加 5 个 Double 对象。接着使用 while 循环遍历 scores 集合对象，输出该对象中的元素，然后调用 TreeSet 类中的 contains() 方法获取该集合中是否存在指定的元素。最后分别调用 TreeSet 类中的 headSet() 方法和 tailSet() 方法获取不及格的成绩和 90 分以上的成绩。

运行该程序，执行结果如下所示。

```
------------学生成绩管理系统-------------
第1个学生成绩：
53
第2个学生成绩：
48
第3个学生成绩：
85
第4个学生成绩：
98
第5个学生成绩：
68
学生成绩从低到高的排序为：
48.0    53.0    68.0    85.0    98.0   
请输入要查询的成绩：
90
成绩为： 90.0 的学生不存在！

不及格的成绩有：
48.0    53.0   
90 分以上的成绩有：
98.0   
```

注意：在使用自然排序时只能向 TreeSet 集合中添加相同数据类型的对象，否则会抛出 ClassCastException 异常。如果向 TreeSet 集合中添加了一个 Double 类型的对象，则后面只能添加 Double 对象，不能再添加其他类型的对象，例如 String 对象等。