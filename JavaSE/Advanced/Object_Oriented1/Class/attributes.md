# 属性

类的属性有以下三种：

(1) 公有属性：在类中和类外都能调用的属性称为公有属性
(2) 私有属性：不能在类外及被类以外的函数调用，只能在类的内部调用的属性称为私有属性，必须以双下划线开始来定义私有属性，如 __name，__age 等
(3) 内置属性：由系统在定义类的时候默认添加的属性称为内置属性，内置属性由前后双下划线构成，如 __dic__ ，__module__ 等

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

class People(object):
    def __init__(self):
        self.name = 'Tom'    # 定义公有属性
        self.__age = 23      # 定义私有属性

    def talk(self):
        print("My name is %s" % self.name)    # 可以在类的内部调用公有属性
        print("My age is %d" % self.__age)    # 可以在类的内部调用私有属性

ren = People()print(ren.name)     # 可以通过对象在类的外部调用公有属性
print(ren.__age)    # 不可以通过对象在类的外部调用私有属性，这里会报错
```