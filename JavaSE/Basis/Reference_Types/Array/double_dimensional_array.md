# 二维数组

在 Java 中二维数组被看作数组的数组，即二维数组为一个特殊的一维数组，其每个元素又是一个一维数组。Java 并不直接支持二维数组，但是允许定义数组元素是一维数组的一维数组，以达到同样的效果。

**二维数组内存结构**：

![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202209182037258.jpeg)

## 二维数组声明

声明二维数组的**语法形式**：

```java
type arrayName[][];    // 数据类型 数组名[][];
```

或

```java
type[][] arrayName;    // 数据类型[][] 数组名;
```

- type 表示二维数组的类型
- arrayName 表示数组名称
- 第一个中括号表示行
- 第二个中括号表示列。

分别声明 int 类型和 char 类型的数组：

```java
int[][] age;
char[][] sex;
```

## 二维数组初始化

### 定义时初始化

**语法格式**：

```java
type[][] arrayName = new type[][]{值 1,值 2,值 3,…,值 n};    // 在定义时初始化
```

**例**：

```
int[][] temp = new int[][]{{1,2},{3,4}};
```

上述代码创建了一个二行二列的二维数组 temp，并对数组中的元素进行了初始化。

### 指定数组大小后初始化

**语法格式**：

```java
type[][] arrayName = new type[size1][size2];    // 给定空间，在赋值
```

例：

```
int[][] temp = new int[2][2];
```

上述代码创建了一个二行二列的二维数组 temp，并对数组中的元素进行了初始化。

### 不指定列数初始化

**语法格式**：

```java
type[][] arrayName = new type[size][];    // 数组第二维长度为空，可变化
```

**例**：

```
int[][] temp = new int[2][];
```

上述代码创建了一个二行的二维数组 temp，并对数组中的元素进行了初始化。

## 获取单个元素

当需要获取二维数组中元素的值时，也可以使用下标来表示。

**语法格式**：

```java
arrayName[i-1][j-1];
```

- arrayName 表示数组名称
- i 表示数组的行数
- j 表示数组的列数。

要获取第二行第二列元素的值，应该使用 `temp[1][1]`来表示。这是由于数组的下标起始值为 0，因此行和列的下标需要减 1。

**例**：

通过下标获取 class_score 数组中第二行第二列元素的值与第四行第一列元素的值。代码如下：

```java
public static void main(String[] args) {    
    double[][] class_score = {{10.0,99,99},{100,98,97},{100,100,99.5},{99.5,99,98.5}}; 
    System.out.println("第二行第二列元素的值："+class_score[1][1]);    
    System.out.println("第四行第一列元素的值："+class_score[3][0]);
}
```

输出结果：

> 第二行第二列元素的值：98.0
> 第四行第一列元素的值：99.5

## 获取整行元素

获取指定行的元素时，需要将行数固定，然后只遍历该行中的全部列即可。

**例**：编写一个案例，接收用户在控制台输入的行数，然后获取该行中所有元素的值：

```java
public static void main(String[] args) {    
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } }; 
    Scanner scan = new Scanner(System.in);    
    System.out.println("当前数组只有" + class_score.length + "行，您想查看第几行的元素？请输入：");    
    int number = scan.nextInt();    
    for (int j = 0; j < class_score[number - 1].length; j++) {        
        System.out.println("第" + number + "行的第[" + j + "]个元素的值是：" + class_score[number - 1][j]); 
    }
}
```

输出结果：

> 当前数组只有4行，您想查看第几行的元素？请输入：
> 3
> 第3行的第[0]个元素的值是：100.0
> 第3行的第[1]个元素的值是：100.0
> 第3行的第[2]个元素的值是：99.5

## 获取整列元素

获取指定列的元素与获取指定行的元素相似，保持列不变，遍历每一行的该列即可。

**例**：编写一个案例，接收用户在控制台中输入的列数，然后获取二维数组中所有行中该列的值：

```java
public static void main(String[] args) {    
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } }; 
    Scanner scan = new Scanner(System.in);    
    System.out.println("您要获取哪一列的值？请输入：");    
    int number = scan.nextInt();    
    for (int i = 0; i < class_score.length; i++) {        
        System.out.println("第 " + (i + 1) + " 行的第[" + number + "]个元素的值是" + class_score[i][number]); 
    }
}
```

执行结果：

> 您要获取哪一列的值？请输入：
> 2
> 第 1 行的第[2]个元素的值是99.0
> 第 2 行的第[2]个元素的值是97.0
> 第 3 行的第[2]个元素的值是99.5
> 第 4 行的第[2]个元素的值是98.5

## 获取全部元素

在一维数组中直接使用数组的 length 属性获取数组元素的个数。而在二维数组中，直接使用 length 属性获取的是数组的行数，在指定的索引后加上 length(如 `array[0].length`)表示的是该行拥有多少个元素，即列数。

如果要获取二维数组中的全部元素，最简单、最常用的办法就是使用 for 语句。在一维数组全部输出时，我们使用一层 for 循环，而二维数组要想全部输出，则使用嵌套 for 循环(2 层 for 循环)。

**例**：

1. 使用 [for 循环语句](../../Process_Control/Loop_Structure/for.md)遍历 double 类型的 class_score 数组的元素，并输出每一行每一列元素的值：

   ```java
   public static void main(String[] args) {    
       double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } };    
       for (int i = 0; i < class_score.length; i++) { // 遍历行        
           for (int j = 0; j < class_score[i].length; j++) {            
               System.out.println("class_score[" + i + "][" + j + "]=" +class_score[i][j]);        
           }    
       }
   }
   ```

   使用嵌套 for 循环语句输出二维数组。在输出二维数组时，第一个 for 循环语句表示以行进行循环，第二个 for 循环语句表示以列进行循环，这样就实现了获取二维数组中每个元素的值的功能。

   输出结果：

   > `class_score[0][0]=100.0`
   > `class_score[0][1]=99.0`
   > `class_score[0][2]=99.0`
   > `class_score[1][0]=100.0`
   > `class_score[1][1]=98.0`
   > `class_score[1][2]=97.0`
   > `class_score[2][0]=100.0`
   > `class_score[2][1]=100.0`
   > `class_score[2][2]=99.5`
   > `class_score[3][0]=99.5`
   > `class_score[3][1]=99.0`
   > `class_score[3][2]=98.5`

2. 假设有一个矩阵为 5 行 5 列，该矩阵是由程序随机产生的 10 以内数字排列而成：

   ```java
   public class Test11 {    
       public static void main(String[] args) {        
           // 创建一个二维矩阵        
           int[][] matrix = new int[5][5];        
           // 随机分配值        
           for (int i = 0; i < matrix.length; i++) {            
               for (int j = 0; j < matrix[i].length; j++) {                
                   matrix[i][j] = (int) (Math.random() * 10);            
               }        
           }        
           System.out.println("下面是程序生成的矩阵\n");        
           // 遍历二维矩阵并输出        
           for (int k = 0; k < matrix.length; k++) {            
               for (int g = 0; g < matrix[k].length; g++) {                
                   System.out.print(matrix[k][g] + "");            
               }            
               System.out.println();        
           }    
       }
   }
   ```

   在该程序中，首先定义了一个二维数组，然后使用两个嵌套的 for 循环向二维数组中的每个元素赋值。其中，`Math.random()` 方法返回的是一个 double 类型的数值，数值为 0.6、0.9 等，因此乘以 10 之后为 10 以内的整数。最后又使用了两个嵌套的 for 循环遍历二维数组，输出二维数组中的值，从而产生矩阵。

   运行结果：

   > 下面是程序生成的矩阵
   >
   > 78148
   > 69230
   > 43823
   > 75663
   > 05688

------

[for each 循环语句](../../Process_Control/Loop_Structure/foreach.md)不能自动处理二维数组的每一个元素。它是按照行， 也就是一维数组处理的。要想访问二维教组 a 的所有元素， 需要使用两个嵌套的循环：

```java
for (double[] row : a) {    
    for (double value : row) {        
        ......    
    }
}
```

**例**：

```java
public static void main(String[] args) {    
    double[][] class_score = { { 100, 99, 99 }, { 100, 98, 97 }, { 100, 100, 99.5 }, { 99.5, 99, 98.5 } }; 
    for (double[] row : class_score) {        
        for (double value : row) {            
            System.out.println(value);        
        }    
    }
}
```

输出结果为：

> 100.0
> 99.0
> 99.0
> 100.0
> 98.0
> 97.0
> 100.0
> 100.0
> 99.5
> 99.5
> 99.0
> 98.5

**提示**：要想快速地打印一个二维数组的数据元素列表([Array工具类](../../../Advanced/Object_Oriented/Class/Commonly_Class/Arrays/README.md))，可以调用：

```java
System.out.println(Arrays.deepToString(arrayName));
```

**例**：

```
System.out.println(Arrays.deepToString(class_score));
```

输出格式：

> [[100.0, 99.0, 99.0], [100.0, 98.0, 97.0], [100.0, 100.0, 99.5], [99.5, 99.0, 98.5]]