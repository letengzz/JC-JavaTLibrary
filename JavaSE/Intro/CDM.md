# Java两种核心机制

## Java虚拟机(`Java Virtal Machine`)

JVM是一个虚拟的计算机,具有指令集并使用不同的存储区域。负责执行指令,管理数据、内存、寄存器。

对于不同的平台,有不同的虚拟机。

只有某平台提供了对应的java虚拟机, java程序才可在此平台运行.

Java虚拟机机制屏敲了底层运行平台的差别,实现了"一次编译,到处运行"

![image-20220720192913057](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211139595.png)

![image-20220720192931884](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207251924743.png)

## 垃圾收集机制(`Garbage Collection`)

不再使用的内存空间应回收-垃圾回收。

在C/C++等语言中,由程序员负责回收无用内存。

Java语言消除了程序员回收无用内存空间的责任:它提供一种系统级线程跟踪存储空间的分配情况。并在JVM空闲

时,检查并释放那些可被释放的存储空间。

垃圾回收在Java程序运行过程中自动进行,程序员无法精确控制和干预。