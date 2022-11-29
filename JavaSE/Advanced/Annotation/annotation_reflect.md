# 利用反射获取注解信息

JDK 5.0 在 `java.lang.reflect` 包下新增了 AnnotatedElement 接口，**该接口代表程序中可以接受注解的程序元素**。 当一个 Annotation 类型被定义为运行时 Annotation 后，该注解才是**运行时可见**，当 class 文件被载入时保存在 class 文件中的 Annotation 才会被虚拟机读取。 程序可以调用 AnnotatedElement对象的如下方法来访问 Annotation 信息。

![image-20221109205324064](https://raw.githubusercontent.com/letengzz/Two-C/main/img/Java/202211092057326.png)