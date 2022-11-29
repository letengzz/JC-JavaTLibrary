# 注解

从 Java 5 开始，Java 增加了对元数据(MetaData)的支持，也就是注解(`Annotation`)。**注解是Java语言用于工具处理的标注**。。[注解](annotation_concept.md)与[注释](../../Basis/Basic_Grammar/comment.md)是有一定区别的，可以把注解理解为代码里的特殊标记，这些标记可以**在编译、类加载和运行时被读取，并执行相应的处理**。可以通过注解**在不改变原有代码和逻辑的情况下在源代码中嵌入补充信息**。

- [注解概念及作用](annotation_concept.md)
- [自定义注解](annotation_custom.md)
- [生成文档相关的注解(JavaDoc)](../../Basis/Basic_Grammar/JavaDoc/README.md)
- [通过反射获取注解信息](annotation_reflect.md)

**内置注解**：

- **基本注解**：[@Override注解](Built_in/Basic/Override.md)
- **基本注解**：[@Deprecated注解](Built_in/Basic/Deprecated.md)
- **基本注解**：[@SuppressWarnings注解](Built_in/Basic/SuppressWarnings.md)
- **基本注解**：[@SafeVarargs](Built_in/Basic/SafeVarargs.md)
- **基本注解**：[@Functionallnterface](Built_in/Basic/FunctionalInterface.md)

- **元注解**：[@Retention](Built_in/Meta/README.md#@Retention)

- **元注解**：[@Target](Built_in/Meta/README.md#@Target)
- **元注解**：[@Documented](Built_in/Meta/README.md#@Documented)
- **元注解**：[@Inherited](Built_in/Meta/README.md#@Inherited)
- **元注解**：[@Native](Built_in/Meta/README.md#@Native)
- **元注解**：[@Repeatable](Built_in/Meta/README.md#@Repeatable)