# Collection接口

Collection 接口是 List、Set 和 Queue 接口的父接口，通常情况下不被直接使用。Collection 接口定义了一些通用的方法，通过这些方法可以实现对集合的基本操作。定义的方法既可用于操作 Set 集合，也可用于操作 List 和 Queue 集合。

本节将介绍 Collection 接口中常用的方法，如表 1 所示。



| 方法名称                          | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| boolean add(E e)                  | 向集合中添加一个元素，如果集合对象被添加操作改变了，则返回 true。E 是元素的数据类型 |
| boolean addAll(Collection c)      | 向集合中添加集合 c 中的所有元素，如果集合对象被添加操作改变了，则返回 true。 |
| void clear()                      | 清除集合中的所有元素，将集合长度变为 0。                     |
| boolean contains(Object o)        | 判断集合中是否存在指定元素                                   |
| boolean containsAll(Collection c) | 判断集合中是否包含集合 c 中的所有元素                        |
| boolean isEmpty()                 | 判断集合是否为空                                             |
| Iterator<E>iterator()             | 返回一个 Iterator 对象，用于遍历集合中的元素                 |
| boolean remove(Object o)          | 从集合中删除一个指定元素，当集合中包含了一个或多个元素 o 时，该方法只删除第一个符合条件的元素，该方法将返回 true。 |
| boolean removeAll(Collection c)   | 从集合中删除所有在集合 c 中出现的元素（相当于把调用该方法的集合减去集合 c）。如果该操作改变了调用该方法的集合，则该方法返回 true。 |
| boolean retainAll(Collection c)   | 从集合中删除集合 c 里不包含的元素（相当于把调用该方法的集合变成该集合和集合 c 的交集），如果该操作改变了调用该方法的集合，则该方法返回 true。 |
| int size()                        | 返回集合中元素的个数                                         |
| Object[] toArray()                | 把集合转换为一个数组，所有的集合元素变成对应的数组元素。     |


注意：以上方法完全来自于 [Java](http://c.biancheng.net/java/) API 文档，读者可自行参考 API 文档来查阅这些方法的详细信息。读者无需硬性记忆这些方法，可以和实际生活结合记忆。集合类就像容器，现实生活中容器的功能，就是添加对象、删除对象、清空容器和判断容器是否为空等，集合类为这些功能都提供了对应的方法。

#### 例 1

经过前面的介绍，我们知道 Collection 是非常重要的一个接口，在表 1 中列出了其常用方法。本案例将编写一个简单的程序，演示如何使用 Collection 接口向集合中添加方法。具体实现代码如下：

```
public static void main(String[] args) {    ArrayList list1 = new ArrayList(); // 创建集合 list1    ArrayList list2 = new ArrayList(); // 创建集合 list2    list1.add("one"); // 向 list1 添加一个元素    list1.add("two"); // 向 list1 添加一个元素    list2.addAll(list1); // 将 list1 的所有元素添加到 list2    list2.add("three"); // 向 list2 添加一个元素    System.out.println("list2 集合中的元素如下：");    Iterator it1 = list2.iterator();    while (it1.hasNext()) {        System.out.print(it1.next() + "、");    }}
```

由于 Collection 是接口，不能对其实例化，所以上述代码中使用了 Collection 接口的 ArrayList 实现类来调用 Collection 的方法。add() 方法可以向 Collection 中添加一个元素，而调用 addAll() 方法可以将指定 Collection 中的所有元素添加到另一个 Collection 中。

代码创建了两个集合 list1 和 list2，然后调用 add() 方法向 list1 中添加了两个元素，再调用 addAll() 方法将这两个元素添加到 list2 中。接下来又向 list2 中添加了一个元素，最后输出 list2 集合中的所有元素，结果如下：

```
list2 集合中的元素如下：
one、two、three、
```

#### 例 2

创建一个案例，演示 Collection 集合中 size()、remove() 和 removeAll() 方法的应用。具体代码如下：

```
public static void main(String[] args) {    ArrayList list1 = new ArrayList(); // 创建集合 list1    ArrayList list2 = new ArrayList(); // 创建集合 list2    list1.add("one");    list1.add("two");    list1.add("three");    System.out.println("list1 集合中的元素数量：" + list1.size()); // 输出list1中的元素数量    list2.add("two");    list2.add("four");    list2.add("six");    System.out.println("list2 集合中的元素数量：" + list2.size()); // 输出list2中的元素数量    list2.remove(2); // 删除第 3 个元素    System.out.println("\nremoveAll() 方法之后 list2 集合中的元素数量：" + list2.size());    System.out.println("list2 集合中的元素如下：");    Iterator it1 = list2.iterator();    while (it1.hasNext()) {        System.out.print(it1.next() + "、");    }    list1.removeAll(list2);    System.out.println("\nremoveAll() 方法之后 list1 集合中的元素数量：" + list1.size());    System.out.println("list1 集合中的元素如下：");    Iterator it2 = list1.iterator();    while (it2.hasNext()) {        System.out.print(it2.next() + "、");    }}
```

list2 集合在调用 remove(2) 方法删除第 3 个元素之后剩下了 two 和 four。list1.removeAll(list2) 语句会从 list1 中将 list1 和 list2 中相同的元素删除，即删除 two 元素。最后输出结果如下：

```
list1 集合中的元素数量：3
list2 集合中的元素数量：3

removeAll() 方法之后 list2 集合中的元素数量：2
list2 集合中的元素如下：
two、four、
removeAll() 方法之后 list1 集合中的元素数量：2
list1 集合中的元素如下：
one、three、
```

注意：retainAll( ) 方法的作用与 removeAll( ) 方法相反，即保留两个集合中相同的元素，其他全部删除。

编译上面程序时，系统可能输出一些警告提示，这些警告是提示用户没有使用泛型来限制集合里的元素类型，读者暂时不要理会这些警告，后面我们会详细介绍泛型编程。

在传统模式下，把一个对象“丢进”集合中后，集合会忘记这个对象的类型。也就是说，系统把所有的集合元素都当成 Object 类型。从 Java 5 以后，可以使用泛型来限制集合里元素的类型，并让集合记住所有集合元素的类型。关于泛型，可参考《[Java泛型详解](http://c.biancheng.net/view/1085.html)》一节。