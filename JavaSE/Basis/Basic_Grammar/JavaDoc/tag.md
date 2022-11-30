# Javadoc标签

Javadoc 工具可以识别文档注释中的一些特殊标签，这些标签一般以`@`开头，后跟一个指定的名字，有的也以`{@`开头，以`}`结束。Javadoc 可以识别的标签如下表所示：

对两种标签格式的说明：

![202211071709722.png](https://github.com/letengzz/Two-C/blob/main/img/Java/202211071709722.png?raw=true)

- `@tag` 格式的标签（不被`{ }`包围的标签）为块标签，只能在主要描述（类注释中对该类的详细说明为主要描述）后面的标签部分（如果块标签放在主要描述的前面，则生成 API 帮助文档时会检测不到主要描述）。

- `{@tag}` 格式的标签（由`{ }`包围的标签）为内联标签，可以放在主要描述中的任何位置或块标签的注释中。

-  `@param` `@return` 和 `@exception` 这三个标记都是只用于方法的

  `@param`的格式要求：`@param 形参名 形参类型 形参说明；` 

  `@return` 的格式要求：`@return 返回值类型 返回值说明；` 

  `@exception`的格式要求：`@exception 异常类型 异常说明；` 

  `@param`和`@exception`可以并列多个。


Javadoc 标签**注意事项**：

- Javadoc 标签必须从一行的开头开始，否则将被视为普通文本。
- 一般具有相同名称的标签放在一起。
- Javadoc 标签区分大小写，代码中对于大小写错误的标签不会发生编译错误，但是在生成 API 帮助文档时会检测不到该注释内容。
