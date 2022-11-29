# serialVersionUID

如果可序列化类没有显式声明serialVersionUID，那么序列化运行时将根据类的各个方面为该类计算一个缺省的serialVersionUID值，如Java对象序列化规范中所述。 该规范将枚举类型的serialVersionUID定义为0L。 然而，强烈建议除enum类型之外的所有可序列化类显式声明serialVersionUID值，因为默认的serialVersionUID计算对类细节非常敏感，这些细节可能因编译器实现而异，因此可能在反序列化期间导致意外的InvalidClassExceptions。 因此，为了保证不同java编译器实现之间的serialVersionUID值一致，可序列化类必须声明显式的serialVersionUID值。 还强烈建议显式serialVersionUID声明在可能的情况下使用私有修饰符，因为这样的声明只适用于立即声明的类——serialVersionUID字段作为继承成员是没有用的。 数组类不能声明显式的serialVersionUID，因此它们总是有默认的计算值，但是数组类放弃了匹配serialVersionUID值的要求。 

## IDEA自动生成serialVersionUID

**setting–>Editor–>Inspections–>JVM languages–>Serializable class without ‘serialVersionUID’**
![image-20221101183920537](D:\Data\typora\photo\image-20221101183920537.png)

直接搜索UID就可以定位到了，勾选即可。

