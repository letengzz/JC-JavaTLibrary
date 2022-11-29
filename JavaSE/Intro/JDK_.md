# JDK、JRE、JSR、JCP

**JDK**：`Java Development Kit`

​	JDK是提供给Java开发人员使用的，其中包含了java的开发工具，也包括了JRE。所以安装了JDK，就不用在单独安装JRE了。、

​	使用JDK的开发工具完成的java程序，交给JRE去运行。

​	其中的开发工具：编译工具(javac.exe) 打包工具(jar.exe)等

**JRE**：`Java Runtime Environment`

​	包括Java虚拟机(JVM `Java Virtual Machine`)和Java程序所需的核心类库等， 如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。

​	简单地说，JRE就是运行Java字节码的虚拟机。但是，如果只有Java源码，要编译成Java字节码，就需要JDK，因为JDK除了包含JRE，还提供了编译器、调试器等开发工具。

**两者的关系**：

![image-20220720105940694](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211140676.png)

![构成](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211140387.png)

![image-20220720192334284](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211140410.png)

------

**JSR**规范：`Java Specification Request`

**JCP**组织：`Java Community Process`

​	为了保证Java语言的规范性，SUN公司搞了一个JSR规范，凡是想给Java平台加一个功能，比如说访问数据库的功能，大家要先创建一个JSR规范，定义好接口，这样，各个数据库厂商都按照规范写出Java驱动程序，开发者就不用担心自己写的数据库代码在MySQL上能跑，却不能跑在PostgreSQL上。

所以JSR是一系列的规范，从JVM的内存模型到Web程序接口，全部都标准化了。而负责审核JSR的组织就是JCP。

​	一个JSR规范发布时，为了让大家有个参考，还要同时发布一个“参考实现”，以及一个“兼容性测试套件”：

**RI**：`Reference Implementation`

**TCK**：`Technology Compatibility Kit`

​	比如有人提议要搞一个基于Java开发的消息服务器，这个提议很好啊，但是光有提议还不行，得贴出真正能跑的代码，这就是RI。如果有其他人也想开发这样一个消息服务器，如何保证这些消息服务器对开发者来说接口、功能都是相同的？所以还得提供TCK。

​	通常来说，RI只是一个“能跑”的正确的代码，它不追求速度，所以，如果真正要选择一个Java的消息服务器，一般是没人用RI的，大家都会选择一个有竞争力的商用或开源产品。

​	参考：Java消息服务JMS的JSR：https://jcp.org/en/jsr/detail?id=914

​	[JDK配置](../develop.md)