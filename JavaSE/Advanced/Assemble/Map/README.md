# Map集合

Map 是一种键-值对（key-value）集合，Map 集合中的每一个元素都包含一个键（key）对象和一个值（value）对象。用于保存具有映射关系的数据。

Map 集合里保存着两组值，一组值用于保存 Map 里的 key，另外一组值用于保存 Map 里的 value，key 和 value 都可以是任何引用类型的数据。Map 的 key 不允许重复，value 可以重复，即同一个 Map 对象的任何两个 key 通过 equals 方法比较总是返回 false。

Map 中的 key 和 value 之间存在单向一对一关系，即通过指定的 key，总能找到唯一的、确定的 value。从 Map 中取出数据时，只要给出指定的 key，就可以取出对应的 value。

Map 接口主要有两个实现类：HashMap 类和 TreeMap 类。其中，HashMap 类按哈希算法来存取键对象，而 TreeMap 类可以对键对象进行排序。

Map 接口中提供的常用方法如表 1 所示。



| 方法名称                                 | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| void clear()                             | 删除该 Map 对象中的所有 key-value 对。                       |
| boolean containsKey(Object key)          | 查询 Map 中是否包含指定的 key，如果包含则返回 true。         |
| boolean containsValue(Object value)      | 查询 Map 中是否包含一个或多个 value，如果包含则返回 true。   |
| V get(Object key)                        | 返回 Map 集合中指定键对象所对应的值。V 表示值的数据类型      |
| V put(K key, V value)                    | 向 Map 集合中添加键-值对，如果当前 Map 中已有一个与该 key 相等的 key-value 对，则新的 key-value 对会覆盖原来的 key-value 对。 |
| void putAll(Map m)                       | 将指定 Map 中的 key-value 对复制到本 Map 中。                |
| V remove(Object key)                     | 从 Map 集合中删除 key 对应的键-值对，返回 key 对应的 value，如果该 key 不存在，则返回 null |
| boolean remove(Object key, Object value) | 这是 [Java](http://c.biancheng.net/java/) 8 新增的方法，删除指定 key、value 所对应的 key-value 对。如果从该 Map 中成功地删除该 key-value 对，该方法返回 true，否则返回 false。 |
| Set entrySet()                           | 返回 Map 集合中所有键-值对的 Set 集合，此 Set 集合中元素的数据类型为 Map.Entry |
| Set keySet()                             | 返回 Map 集合中所有键对象的 Set 集合                         |
| boolean isEmpty()                        | 查询该 Map 是否为空（即不包含任何 key-value 对），如果为空则返回 true。 |
| int size()                               | 返回该 Map 里 key-value 对的个数                             |
| Collection values()                      | 返回该 Map 里所有 value 组成的 Collection                    |


Map 集合最典型的用法就是成对地添加、删除 key-value 对，接下来即可判断该 Map 中是否包含指定 key，也可以通过 Map 提供的 keySet() 方法获取所有 key 组成的集合，进而遍历 Map 中所有的 key-value 对。下面程序示范了 Map 的基本功能。

#### 例 1

每名学生都有属于自己的唯一编号，即学号。在毕业时需要将该学生的信息从系统中移除。

下面编写 Java 程序，使用 HashMap 来存储学生信息，其键为学生学号，值为姓名。毕业时，需要用户输入学生的学号，并根据学号进行删除操作。具体的实现代码如下：

```
public class Test09 {    public static void main(String[] args) {        HashMap users = new HashMap();        users.put("11", "张浩太"); // 将学生信息键值对存储到Map中        users.put("22", "刘思诚");        users.put("33", "王强文");        users.put("44", "李国量");        users.put("55", "王路路");        System.out.println("******** 学生列表 ********");        Iterator it = users.keySet().iterator();        while (it.hasNext()) {            // 遍历 Map            Object key = it.next();            Object val = users.get(key);            System.out.println("学号：" + key + "，姓名:" + val);        }        Scanner input = new Scanner(System.in);        System.out.println("请输入要删除的学号：");        int num = input.nextInt();        if (users.containsKey(String.valueOf(num))) { // 判断是否包含指定键            users.remove(String.valueOf(num)); // 如果包含就删除        } else {            System.out.println("该学生不存在！");        }        System.out.println("******** 学生列表 ********");        it = users.keySet().iterator();        while (it.hasNext()) {            Object key = it.next();            Object val = users.get(key);            System.out.println("学号：" + key + "，姓名：" + val);        }    }}
```

在该程序中，两次使用 while 循环遍历 HashMap 集合。当有学生毕业时，用户需要输入该学生的学号，根据学号使用 HashMap 类的 remove() 方法将对应的元素删除。程序运行结果如下所示。

```
******** 学生列表 ********
学号：44，姓名:李国量
学号：55，姓名:王路路
学号：22，姓名:刘思诚
学号：33，姓名:王强文
学号：11，姓名:张浩太
请输入要删除的学号：
22
******** 学生列表 ********
学号：44，姓名：李国量
学号：55，姓名：王路路
学号：33，姓名：王强文
学号：11，姓名：张浩太
******** 学生列表 ********
学号：44，姓名:李国量
学号：55，姓名:王路路
学号：22，姓名:刘思诚
学号：33，姓名:王强文
学号：11，姓名:张浩太
请输入要删除的学号：
44
******** 学生列表 ********
学号：55，姓名：王路路
学号：22，姓名：刘思诚
学号：33，姓名：王强文
学号：11，姓名：张浩太
```


注意：TreeMap 类的使用方法与 HashMap 类相同，唯一不同的是 TreeMap 类可以对键对象进行排序，这里不再赘述。