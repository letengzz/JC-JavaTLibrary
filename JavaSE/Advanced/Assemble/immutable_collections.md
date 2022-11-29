# Java 9新增的不可变集合

[Java](http://c.biancheng.net/java/) 9 版本以前，假如要创建一个包含 6 个元素的 Set 集合，程序需要先创建 Set 集合，然后调用 6 次 add() 方法向 Set 集合中添加元素。Java 9 对此进行了简化，程序直接调用 Set、List、Map 的 of() 方法即可创建包含 N 个元素的不可变集合，这样一行代码就可创建包含 N 个元素的集合。

不可变意味着程序不能向集合中添加元素，也不能从集合中删除元素。

如下程序示范了如何创建不可变集合。

```
public class Java9Collection {    public static void main(String[] args) {        // 创建包含4个元素的Set集合        Set set = Set.of("Java", "Kotlin", "Go", "Swift");        System.out.println(set);        // 不可变集合，下面代码导致运行时错误        // set.add("Ruby");        // 创建包含4个元素的List集合        List list = List.of(34, -25, 67, 231);        System.out.println(list);        // 不可变集合，下面代码导致运行时错误        // list.remove(1);        // 创建包含3个key-value对的Map集合        Map map = Map.of("语文", 89, "数学", 82, "英语", 92);        System.out.println(map);        // 不可变集合，下面代码导致运行时错误        // map.remove("语文");        // 使用Map.entry()方法显式构建key-value对        Map map2 = Map.ofEntries(Map.entry("语文", 89), Map.entry("数学", 82), Map.entry("英语", 92));        System.out.println(map2);    }}
```

上面第 4、9、14 和 19 行代码示范了如何使用集合元素创建不可变集合，其中 Set、List 比较简单，程序只要为它们的 of() 方法传入 N 个集合元素即可创建 Set、List 集合。

从上面代码可以看出，创建不可变的 Map 集合有两个方法。使用 of() 方法时只要依次传入多个 key-value 对即可；还可使用 ofEntries() 方法，该方法可接受多个 Entry 对象，因此程序显式使用 Map.entry() 方法来创建 Map.Entry 对象。