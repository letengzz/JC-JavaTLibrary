# 使用Java 8新增的Stream操作Collection集合

[Java](http://c.biancheng.net/java/) 8 还新增了 Stream、IntStream、LongStream、DoubleStream 等流式 API，这些 API 代表多个支持串行和并行聚集操作的元素。上面 4 个接口中，Stream 是一个通用的流接口，而 IntStream、LongStream、 DoubleStream 则代表元素类型为 int、long、double 的流。

Java 8 还为上面每个流式 API 提供了对应的 Builder，例如 Stream.Builder、IntStream.Builder、LongStream.Builder、DoubleStream.Builder，开发者可以通过这些 Builder 来创建对应的流。

独立使用 Stream 的步骤如下：

1. 使用 Stream 或 XxxStream 的 builder() 类方法创建该 Stream 对应的 Builder。
2. 重复调用 Builder 的 add() 方法向该流中添加多个元素。
3. 调用 Builder 的 build() 方法获取对应的 Stream。
4. 调用 Stream 的聚集方法。


在上面 4 个步骤中，第 4 步可以根据具体需求来调用不同的方法，Stream 提供了大量的聚集方法供用户调用，具体可参考 Stream 或 XxxStream 的 API 文档。对于大部分聚集方法而言，每个 Stream 只能执行一次。例如如下程序。

```
public class IntStreamTest {    public static void main(String[] args) {        IntStream is = IntStream.builder().add(20).add(13).add(-2).add(18).build();        // 下面调用聚集方法的代码每次只能执行一行        System.out.println("is 所有元素的最大值：" + is.max().getAsInt());        System.out.println("is 所有元素的最小值：" + is.min().getAsInt());        System.out.println("is 所有元素的总和：" + is.sum());        System.out.println("is 所有元素的总数：" + is.count());        System.out.println("is 所有元素的平均值：" + is.average());        System.out.println("is所有元素的平方是否都大于20: " + is.allMatch(ele -> ele * ele > 20));        System.out.println("is是否包含任何元素的平方大于20 : " + is.anyMatch(ele -> ele * ele > 20));        // 将is映射成一个新Stream,新Stream的每个元素是原Stream元素的2倍+1        IntStream newIs = is.map(ele -> ele * 2 + 1);        // 使用方法引用的方式来遍历集合元素        newIs.forEach(System.out::println); // 输岀 41 27 -3 37    }}
```

上面程序先创建了一个 IntStream，接下来分别多次调用 IntStream 的聚集方法执行操作，这样即可获取该流的相关信息。注意：上面 5~13 行代码每次只能执行一行，因此需要把其他代码注释掉。

Stream 提供了大量的方法进行聚集操作，这些方法既可以是“中间的”（intermediate），也可以是 "末端的"（terminal）。

- 中间方法：中间操作允许流保持打开状态，并允许直接调用后续方法。上面程序中的 map() 方法就是中间方法。中间方法的返回值是另外一个流。
- 末端方法：末端方法是对流的最终操作。当对某个 Stream 执行末端方法后，该流将会被“消耗”且不再可用。上面程序中的 sum()、count()、average() 等方法都是末端方法。


除此之外，关于流的方法还有如下两个特征。

- 有状态的方法：这种方法会给流增加一些新的属性，比如元素的唯一性、元素的最大数量、保证元素以排序的方式被处理等。有状态的方法往往需要更大的性能开销。
- 短路方法：短路方法可以尽早结束对流的操作，不必检查所有的元素。


下面简单介绍一下 Stream 常用的中间方法。

| 方法                           | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| filter(Predicate predicate)    | 过滤 Stream 中所有不符合 predicate 的元素                    |
| mapToXxx(ToXxxFunction mapper) | 使用 ToXxxFunction 对流中的元素执行一对一的转换，该方法返回的新流中包含了 ToXxxFunction 转换生成的所有元素。 |
| peek(Consumer action)          | 依次对每个元素执行一些操作，该方法返回的流与原有流包含相同的元素。该方法主要用于调试。 |
| distinct()                     | 该方法用于排序流中所有重复的元素（判断元素重复的标准是使用 equals() 比较返回 true）。这是一个有状态的方法。 |
| sorted()                       | 该方法用于保证流中的元素在后续的访问中处于有序状态。这是一个有状态的方法。 |
| limit(long maxSize)            | 该方法用于保证对该流的后续访问中最大允许访问的元素个数。这是一个有状态的、短路方法。 |


下面简单介绍一下 Stream 常用的末端方法。

| 方法                           | 说明                                                       |
| ------------------------------ | ---------------------------------------------------------- |
| forEach(Consumer action)       | 遍历流中所有元素，对每个元素执行action                     |
| toArray()                      | 将流中所有元素转换为一个数组                               |
| reduce()                       | 该方法有三个重载的版本，都用于通过某种操作来合并流中的元素 |
| min()                          | 返回流中所有元素的最小值                                   |
| max()                          | 返回流中所有元素的最大值                                   |
| count()                        | 返回流中所有元素的数量                                     |
| anyMatch(Predicate predicate)  | 判断流中是否至少包含一个元素符合 Predicate 条件。          |
| allMatch(Predicate predicate)  | 判断流中是否每个元素都符合 Predicate 条件                  |
| noneMatch(Predicate predicate) | 判断流中是否所有元素都不符合 Predicate 条件                |
| findFirst()                    | 返回流中的第一个元素                                       |
| findAny()                      | 返回流中的任意一个元素                                     |


除此之外，Java 8 允许使用流式 API 来操作集合，Collection 接口提供了一个 stream() 默认方法，该方法可返回该集合对应的流，接下来即可通过流式 API 来操作集合元素。由于 Stream 可以对集合元素进行整体的聚集操作，因此 Stream 极大地丰富了集合的功能。

例如，对于《[Predicate操作collection集合](http://c.biancheng.net/view/6802.html)》一节的示例程序需要额外定义一个 calAll() 方法来遍历集合元素，然后依次对每个集合元素进行判断，这样做太麻烦了。如果使用 Stream 可以直接对集合中所有的元素进行批量操作。下面使用 Stream 来改写这个程序。

```
public class CollectionStream {    public static void main(String[] args) {        // 创建一个集合        Collection objs = new HashSet();        objs.add(new String("C语言中文网Java教程"));        objs.add(new String("C语言中文网C++教程"));        objs.add(new String("C语言中文网C语言教程"));        objs.add(new String("C语言中文网Python教程"));        objs.add(new String("C语言中文网Go教程"));        // 统计集合中出现“C语言中文网”字符串的数量        System.out.println(objs.stream().filter(ele -> ((String) ele).contains("C语言中文网")).count()); // 输出 5        // 统计集合中出现“Java”字符串的数量        System.out.println(objs.stream().filter(ele -> ((String) ele).contains("Java")).count()); // 输出 1        // 统计集合中出现字符串长度大于 12 的数量        System.out.println(objs.stream().filter(ele -> ((String) ele).length() > 12).count()); // 输出 1        // 先调用Collection对象的stream ()方法将集合转换为Stream        // 再调用Stream的mapToInt()方法获取原有的Stream对应的IntStream        objs.stream().mapToInt(ele -> ((String) ele).length())                // 调用forEach()方法遍历IntStream中每个元素                .forEach(System.out::println);// 输出 11 11 12 10 14    }}
```

输出结果为：

5  1  1  11  11  12  10  14

从上面代码第 11~20 行可以看出，程序只要调用 Collection 的 stream() 方法即可返回该集合对应的 Stream，接下来就可通过 Stream 提供的方法对所有集合元素进行处理，这样大大地简化了集合编程的代码，这也是 Stream 编程带来的优势。

上面程序中第 18 行代码先调用 Collection 对象的 stream() 方法将集合转换为 Stream 对象，然后调用 Stream 对象的 mapToInt() 方法将其转换为 IntStream 这个 mapToInt。方法就是一个中间方法，因此程序可继续调用 IntStream 的 forEach() 方法来遍历流中的元素。