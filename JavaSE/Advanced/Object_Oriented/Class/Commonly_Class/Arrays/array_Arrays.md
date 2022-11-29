# Arrays工具类

Arrays 类是一个工具类，其中包含了数组操作的很多方法。这个 Arrays 类里均为 static 修饰的方法（static 修饰的方法可以直接通过类名调用），可以直接通过 Arrays.xxx(xxx) 的形式调用方法。

## 1）int binarySearch(type[] a, type key)

使用二分法查询 key 元素值在 a 数组中出现的索引，如果 a 数组不包含 key 元素值，则返回负数。调用该方法时要求数组中元素己经按升序排列，这样才能得到正确结果。

## 2）int binarySearch(type[] a, int fromIndex, int toIndex, type key)

这个方法与前一个方法类似，但它只搜索 a 数组中 fromIndex 到 toIndex 索引的元素。调用该方法时要求数组中元素己经按升序排列，这样才能得到正确结果。

## 3）type[] copyOf(type[] original, int length)

这个方法将会把 original 数组复制成一个新数组，其中 length 是新数组的长度。如果 length 小于 original 数组的长度，则新数组就是原数组的前面 length 个元素，如果 length 大于 original 数组的长度，则新数组的前面元索就是原数组的所有元素，后面补充 0（数值类型）、false（布尔类型）或者 null（引用类型）。

## 4）type[] copyOfRange(type[] original, int from, int to)

这个方法与前面方法相似，但这个方法只复制 original 数组的 from 索引到 to 索引的元素。

## 5）boolean equals(type[] a, type[] a2)

如果 a 数组和 a2 数组的长度相等，而且 a 数组和 a2 数组的数组元素也一一相同，该方法将返回 true。

## 6）void fill(type[] a, type val)

该方法将会把 a 数组的所有元素都赋值为 val。

## 7）void fill(type[] a, int fromIndex, int toIndex, type val)

该方法与前一个方法的作用相同，区别只是该方法仅仅将 a 数组的 fromIndex 到 toIndex 索引的数组元素赋值为 val。

## 8）void sort(type[] a)

该方法对 a 数组的数组元素进行排序。

## 9）void sort(type[] a, int fromIndex, int toIndex)

该方法与前一个方法相似，区别是该方法仅仅对 fromIndex 到 toIndex 索引的元素进行排序。

#### 10）String toString(type[] a)

该方法将一个数组转换成一个字符串。该方法按顺序把多个数组元素连缀在一起，多个数组元素使用英文逗号`,`和空格隔开。

下面程序示范了 Arrays 类的用法。

```
public class ArraysTest {    public static void main(String[] args) {        // 定义一个a数组        int[] a = new int[] { 3, 4, 5, 6 };        // 定义一个a2数组        int[] a2 = new int[] { 3, 4, 5, 6 };        // a数组和a2数组的长度相等，毎个元素依次相等，将输出true        System.out.println("a数组和a2数组是否相等：" + Arrays.equals(a, a2));        // 通过复制a数组，生成一个新的b数组        int[] b = Arrays.copyOf(a, 6);        System.out.println("a数组和b数组是否相等：" + Arrays.equals(a, b));        // 输出b数组的元素，将输出[3, 4, 5, 6, 0, 0]        System.out.println("b 数组的元素为：" + Arrays.toString(b));        // 将b数组的第3个元素（包括）到第5个元素（不包括）賦值为1        Arrays.fill(b, 2, 4, 1);        // 输出b数组的元素，将输出[3, 4, 1, 1, 0, 0]        System.out.println("b 数组的元素为：" + Arrays.toString(b));        // 对b数组进行排序        Arrays.sort(b);        // 输出b数组的元素.将输出[0,0,1,1,3,4]        System.out.println("b数组的元素为：" + Arrays.toString(b));    }}
```

Arrays 类处于 java.util 包下，为了在程序中使用 Arrays 类，必须在程序中导入 java.util.Arrays 类。

除此之外，在 System 类里也包含了一个`static void arraycopy(Object src, int srePos, Object dest, int dcstPos, int length)`方法，该方法可以将 src 数组里的元素值赋给 dest 数组的元素，其中 srcPos 指定从 src 数组的第几个元素开始赋值，length 参数指定将 src 数组的多少个元素值赋给 dest 数组的元素。

[Java](http://c.biancheng.net/java/) 8 增强了 Arrays 类的功能，为 Arrays 类增加了一些工具方法，这些工具方法可以充分利用多 CPU 并行的能力来提高设值、排序的性能。下面是 Java 8 为 Arrays 类增加的工具方法。

提示：由于计算机硬件的飞速发展，目前几乎所有家用 PC 都是 4 核、8 核的 CPU，而服务器的 CPU 则具有更好的性能，因此 Java 8 与时俱进地增加了并发支持，并发支持可以充分利用硬件设备来提高程序的运行性能。

#### 1）oid parallelPrefix(xxx[] array, XxxBinaryOperator op)

该方法使用 op 参数指定的计算公式计算得到的结果作为新的元素。op 计算公式包括 left、right 两个形参，其中 left 代表数组中前一个索引处的元素，right 代表数组中当前索引处的元素，当计算第一个新数组元素时，left 的值默认为 1。

#### 2）void parallelPrefix(xxx[] array, int fromIndex, int toIndex, XxxBinaryOperator op)

该方法与上一个方法相似，区别是该方法仅重新计算 fromIndex 到 toIndex 索引的元素。

#### 3）void setAll(xxx[] array, IntToXxxFunction generator)

该方法使用指定的生成器（generator）为所有数组元素设置值，该生成器控制数组元素的值的生成算法。

#### 4）void parallelSetAll(xxx[] array, IntToXxxFunction generator)

该方法的功能与上一个方法相同，只是该方法增加了并行能力，可以利用多 CPU 并行来提高性能。

#### 5）void parallelSort(xxx[] a)

该方法的功能与 Arrays 类以前就有的 sort() 方法相似，只是该方法增加了并行能力，可以利用多 CPU 并行来提高性能。

#### 6）void parallelSort(xxx[] a，int fromIndex, int toIndex)

该方法与上一个方法相似，区別是该方法仅对 fromIndex 到 toIndex 索引的元素进行排序。

#### 7）Spliterator.OfXxx spliterator(xxx[] array)

将该数组的所有元素转换成对应的 Spliterator 对象。

#### 8）Spliterator.OfXxx spliterator(xxx[] array, int startInclusive, int endExclusive)

该方法与上一个方法相似，区别是该方法仅转换 startInclusive 到 endExclusive 索引的元素。

#### 9）XxxStream stream(xxx[] array)

该方法将数组转换为 Stream，Stream 是 Java 8 新增的流式编程的 API。

#### 10）XxxStream stream(xxx[] array, int startInclusive, int endExclusive)

该方法与上一个方法相似，区别是该方法仅将 fromIndex 到 toIndex 索引的元索转换为 Stream。

上面方法列表中，所有以 parallel 开头的方法都表示该方法可利用 CPU 并行的能力来提高性能。上面方法中的 xxx 代表不同的数据类型，比如处理 int[] 型数组时应将 xxx 换成 int，处理 long[] 型数组时应将 XXX 换成 long。

下面程序示范了 Java 8 为 Arrays 类新增的方法。

下面程序用到了接口、匿名内部类的知识，读者阅读起来可能有一定的困难，此处只要大致知道 Arrays 新增的这些新方法就行，暂时并不需要读者立即掌握该程序，可以等到掌握了接口、匿名内部类后再来学习下面程序。

```
public class ArraysTest2 {    public static void main(String[] args) {        int[] arr1 = new int[] { 3, 4, 25, 16, 30, 18 };        // 对数组arr1进行并发排序        Arrays.parallelSort(arr1);        System.out.println(Arrays.toString(arr1));        int[] arr2 = new int[] { 13, -4, 25, 16, 30, 18 };        Arrays.parallelPrefix(arr2, new IntBinaryOperator() {            // left 代表数组中前一个索引处的元素，计算第一个元素时，left为1            // right代表数组中当前索引处的元素            public int applyAsInt(int left, int right) {                return left * right;            }        });        System.out.println(Arrays.toString(arr2));        int[] arr3 = new int[5];        Arrays.parallelSetAll(arr3, new IntUnaryOperator() {            // operand代表正在计算的元素索引            public int applyAsInt(int operand) {                return operand * 5;            }        });        System.out.println(Arrays.toString(arr3));    }}
```

上面程序中第一行粗体字代码调用了 parallelSort() 方法对数组执行排序，该方法的功能与传统 sort() 方法大致相似，只是在多 CPU 机器上会有更好的性能。

第二段粗体字代码使用的计算公式为 left * right，其中 left 代表数组中当前一个索引处的元素，right 代表数组中当前索引处的元素。程序使用的数组为：

{3, -4 , 25, 16, 30, 18)

计算新的数组元素的方式为：

{1*3=3, 3*-4—12, -12*25=-300, -300*16=—48000, -48000*30=—144000, -144000*18=-2592000}

因此将会得到如下新的数组元素：

{3, -12, -300, -4800, -144000, -2592000)

第三段粗体字代码使用 operand * 5 公式来设置数组元素，该公式中 operand 代表正在计算的数组元素的索引。因此第三段粗体字代码计算得到的数组为：

{0, 5, 10, 15, 20}

提示：上面两段粗体字代码都可以使用 Lambda 表达式进行简化。