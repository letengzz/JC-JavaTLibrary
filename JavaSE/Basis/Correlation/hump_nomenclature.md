# 驼峰命名法

**注意**：大小驼峰的根本区别就在于**首单词的首字母是否大写**，若大写，则是大驼峰命名法;

若是小写，则是小驼峰命名法。

## 大驼峰命名法

​	大驼峰在前，首单词的首字母为大写字母，也就是说构成标识符的所有单词的首字母都大写，其余部分(单词的非首字母部分)都小写。如：`XxxYyyZzz`

## 小驼峰命名法

​	小驼峰在前，首单词的首字母为小写字母，也就是说构成标识符的首单词的首字母小写，其他单词的首字母都大写，且除了单词的首字母外的其他部分都小写。如：`xxxYyyZzz`

## 为啥要用驼峰命名法?

加强代码的可读性

```java
/*在一个学期中,有期中考试,期末考试,如果都像下面这般定义*/
double score1=99,score2=98;
//如何辨别score1和score2中哪个是期中考试成绩的变量还是期末考试的变量呢?显然不好区分
//而用了如下所示的小驼峰命名法,会发现很容易知道它代表的含义及其作用
double midScore=99,finalScore=98;
//mid为中间的意思,final为最终的,那么midScore的含义为中间的成绩即期中成绩,finalScore的含义为最终的成绩即期末考试
```

## 如何使用驼峰命名法

**小驼峰命名法的使用范围**：

​	变量名的命名、函数名(方法名)的命名等

**大驼峰命名法的使用范围**：

​	类名的命名、接口名、命名空间等