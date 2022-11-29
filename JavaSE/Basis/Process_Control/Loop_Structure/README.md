# 循环结构

在某些条件满足的情况下，反复执行特定代码的功能。

循环是程序中的重要流程结构之一。循环语句能够使程序代码重复执行，适用于需要重复一段代码直到满足特定条件为止的情况。

循环语句可以在满足循环条件的情况下，反复执行某一段代码，这段被重复执行的代码被称为**循环体**。当反复执行这个循环体时，需要在合适的时候把循环条件改为假，从而结束循环，否则循环将一直执行下去，形成**死循环**。

**循环语句的四个组成部分**：

- 初始化部分(`init_statement`)： 一条或多条语句，这些语句用于完成一些初始化工作，初始化语句在循环开始之前执行。
- 循环条件部分(`test_expression`)：这是一个 boolean 表达式，这个表达式能决定是否执行循环体。
- 循环体部分(`body_statement`)：这个部分是循环的主体，如果循环条件允许，这个代码块将被重复执行。如果这个代码块只有一行语句，则这个代码块的花括号是可以省略的。
- 迭代部分(`iteration_statement`)：这个部分在一次循环体执行结束后，对循环条件求值之前执行，通常用于控制循环条件中的变量，使得循环在合适的时候结束。

<img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207281458183.png" alt="QGFC2QWFCA_R" style="zoom:67%;" />

上面 4 个部分只是一般性的分类，并不是每个循环中都非常清晰地分出了这 4 个部分。

- [while循环](while.md)
- [do-while循环](do_while.md)
- [while与do-while比较](difference.md)
- [for循环](for.md)

- [for、while、do-while区别](difference.md)

- [foreach](foreach.md)

- [嵌套循环](nested_loops.md)

