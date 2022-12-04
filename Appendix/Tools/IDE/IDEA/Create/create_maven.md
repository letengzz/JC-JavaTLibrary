# 创建Maven工程

- [Maven介绍及使用]()

**IDEA中配置Maven**：

1. 在配置之前，请先[下载-解压-配置Maven]()环境变量等操作。

2. 进入设置，将IDEA中默认的设置路径更改(Maven的目录`Maven home path`、Maven的settings目录`User settings file`、配置仓库`Local repository`)：

   ![7](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011545230.gif)

## 创建普通Maven工程

1. 新建工程：
   ![image-20221201114434991](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011545653.png)
2. IDEA右侧会出现Maven图标，进入可选择各类功能

也可**通过Maven Archetype创建Maven**：

![5](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011545432.gif)

**调整工程结构**：

main目录、test目录需要对应的resources来存放配置文件：

![8](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011553723.gif)

**添加依赖**：

![1](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011633095.gif)

详细操作请参考：[Maven]()

## 创建Maven Web工程

创建过程与创建普通Maven相似，只不过需要将Archetype选项替换为`org.apache.maven.archetypes:maven-archetype-webapp`：

![image-20221201163236264](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202212011632402.png)

创建完成项目后，[配置Tomcat](create_javaweb.md)并部署即可。

**常见问题**：

- **找不到HttpServlet错误**( `The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build Path`)：

  添加依赖：

  ```xml
  <dependency>
  	<groupId>javax.servlet</groupId>
  	<artifactId>servlet-api</artifactId>
  	<version>2.5</version>
  	<scope>provided</scope>
  </dependency>
  ```

- **EL表达式没有提示问题**：

  `${pageContext}`这个EL表达式中通过pageContext对象访问reuqest属性时本身是应该有提示的，但如果没 有的话加入下面依赖即可：

  ```xml
  <dependency>
  	<groupId>javax.servlet.jsp</groupId>
  	<artifactId>jsp-api</artifactId>
  	<version>2.1.3-b06</version>
  	<scope>provided</scope>
  </dependency>
  ```

  针对index.jsp文件修改文件头信息：

  ```jsp
  <%@page language="java" pageEncoding="utf-8" contentType="text/html;UTF-8" %>
  ```

  
