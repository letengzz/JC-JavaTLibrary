# Java开发环境配置

## JDK安装步骤

因为Java程序必须运行在JVM之上，所以，我们第一件事情就是安装JDK。

1. 从[Oracle的官网](https://www.oracle.com/java/technologies/javase-downloads.html)下载最新的稳定版JDK：

   ![image-20220720111309263](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211140164.png)

   ![截.png](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208192117670.png)

   选择自己的设备，下载安装即可！

   - [Java各版本官网下载链接](JDK.md)(JDK 8~JDK 18)

2. 下载完成后，在磁盘中会发现一个名称为 jdk-8u92-windows-x64.exe 的可执行文件。双击该文件，打开 JDK 的欢迎界面：

   ![欢迎界面](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955492.gif)

3. 单击“下一步”按钮，打开定制安装对话框。选择安装的 JDK 组件：

   ![定制安装对话框](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955020.gif)

4. 单击“更改”按钮，可以更改 JDK 的安装路径：

   ![更改安装位置](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955300.gif)

   更改完成之后，单击“下一步”按钮，打开安装进度界面：

   ![显示安装进度](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955569.gif)

5. 在安装过程中会打开如图所示的目标文件夹对话框，选择 JRE 的安装路径，这里使用默认值：

   ![选择JRE安装位置](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955786.gif)

6. 单击“下一步”按钮，安装 JRE。当 JRE 安装完成之后，将打开 JDK 安装完成界面：

   ![安装完成](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955029.gif)

7. 安装完成后，在安装位置打开 JDK 的文件夹，内容和目录结构：

   ![JDK安装目录](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955483.gif)

   从图可以看出，JDK 安装目录下具有多个子目录和一些网页文件，其中重要目录和文件：

   - `bin`：提供 JDK 工具程序，包括 javac、java、javadoc、appletviewer 等可执行程序。
   - `include`：存放用于本地访问的文件。
   - `jre`：存放 Java 运行环境文件。
   - `lib`：存放 Java 的类库文件，工具程序实际上使用的是 Java 类库。JDK 中的工具程序，大多也由 Java 编写而成。
   - `src.zip`：Java 提供的 API 类的源代码压缩文件。如果需要查看 API 的某些功能是如何实现的，可以査看这个文件中的源代码内容。

## 设置环境变量

1. 从桌面上右击"**计算机**"图标，从快捷菜单中选择"**属性**"命令，在打开的"**系统属性**"对话框中单击"**环境变量**"按钮：

<img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955030.png" alt="image-20220821190233627" style="zoom:67%;" />

2.  从弹出的"**环境变量**"对话框中单击"**系统变量**"列表框下方的“新建”按钮：

   <img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211955459.png" alt="image-20220821190636565" style="zoom:67%;" />

3. 弹出"**新建系统变量**"对话框。在“变量名”文本框中输入 `JAVA_HOME`，在"**变量值**"文本框中**输入 JDK 的安装路径**最后单击"**确定**"按钮，保存 `JAVA_HOME` 变量：

   <img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211956687.png" alt="image-20220821192221786" style="zoom:67%;" />

4. 在"**系统变量**"列表框中双击 Path 变量，进入"**编辑系统变量**"对话框。在"**变量值**"文本框的最前端添加：

   ```shell
   %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin
   ```

   <img src="https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202208211956770.png" alt="image-20220821192736551" style="zoom:67%;" />

**注意**：

在比较高的jdk版本中，默认没有jre文件夹，需要手动添加，在`JAVA_HOME`下，使用：

```shell
bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre
```

​	把`JAVA_HOME`的`bin`目录添加到`PATH`中是为了在任意文件夹下都可以运行`java`。打开命令提示符窗口，输入命令`java -version`，如果一切正常，你会看到如下输出：

![image-20220720111553971](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202207211150232.png)
