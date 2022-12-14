# 最凝练的CRUD

## 1.建模

### ①物理建模

> 1.sql

```sql
CREATE DATABASE `view-demo`CHARACTER SET utf8;
USE `view-demo`;
CREATE TABLE t_soldier(
    soldier_id INT PRIMARY KEY AUTO_INCREMENT,
    soldier_name CHAR(100),
    soldier_weapon CHAR(100)
);
```

### ②逻辑建模

> pojo/Soldier.java

```java
public class Soldier {
    private Integer soldierId;
    private String soldierName;
    private String soldierWeapon;
}
```

## 2.总体架构

![./images](data:image/png;base64,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)

## 3.搭建持久化层所需环境

### ①导入jar包

> commons-dbutils-1.6.jar 
>
> druid-1.1.9.jar 
>
> hamcrest-core-1.3.jar 
>
> junit-4.12.jar 
>
> mysql-connector-java-5.1.37-bin.jar

### ②创建jdbc.properties

维护基本连接信息

> jdbc.properties

```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/view-demo
username=root
password=123123
initialSize=10
maxActive=20
maxWait=10000
```

### ③创建JDBCUtils工具类

> JDBCUtil.java

```java
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;

public class JDBCUtil {

    // 将数据源对象设置为静态属性，保证大对象的单一实例
    private static DataSource dataSource;

    static {

        // 1.创建一个用于存储外部属性文件信息的Properties对象
        Properties properties = new Properties();

        // 2.使用当前类的类加载器加载外部属性文件：jdbc.properties
        InputStream inputStream = JDBCUtil.class.getClassLoader().getResourceAsStream("jdbc.properties");

        try {

            // 3.将外部属性文件jdbc.properties中的数据加载到properties对象中
            properties.load(inputStream);

            // 4.创建数据源对象
            dataSource = DruidDataSourceFactory.createDataSource(properties);

        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    /**
     * 从数据源中获取数据库连接
     * @return 数据库连接对象
     */
    public static Connection getConnection() {

        Connection connection = null;

        try {
            connection = dataSource.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();

            throw new RuntimeException(e);
        }

        return connection;

    }

    /**
     * 释放数据库连接
     * @param connection 要执行释放操作的连接对象
     */
    public static void releaseConnection(Connection connection) {

        if (connection != null) {

            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();

                throw new RuntimeException(e);
            }

        }

    }
    
}
```

测试能否正常连接数据库：

> DemoTest.java

```java
public class DemoTest {

    @Test
    public void testConnection() {
        Connection connection = JDBCUtil.getConnection();
        System.out.println("connection = " + connection);
    }

}
```

### ④BaseDao

> BaseDao.java

```java
public class BaseDao<T> {

    private QueryRunner queryRunner = new QueryRunner();

    /**
     * 通用的增删改方法
     * @param sql
     * @param param
     * @return
     */
    public int update(String sql, Object ... param) {

        Connection connection = JDBCUtil.getConnection();

        int count = 0;
        try {
            count = queryRunner.update(connection, sql, param);
        } catch (SQLException e) {
            e.printStackTrace();

            throw new RuntimeException(e);

        } finally {
            
            // 关闭数据库连接
            JDBCUtil.releaseConnection(connection);
            
        }

        return count;
    }

    /**
     * 查询单个对象的通用方法
     * @param clazz
     * @param sql
     * @param param
     * @return
     */
    public T getBean(Class<T> clazz, String sql, Object ... param) {

        Connection connection = JDBCUtil.getConnection();

        T bean = null;
        try {
            bean = queryRunner.query(connection, sql, new BeanHandler<>(clazz), param);
        } catch (SQLException e) {
            e.printStackTrace();
            throw new RuntimeException(e);
        } finally {
            
            // 关闭数据库连接
            JDBCUtil.releaseConnection(connection);
            
        }

        return bean;
    }

    /**
     * 查询集合对象的通用方法
     * @param clazz
     * @param sql
     * @param param
     * @return
     */
    public List<T> getBeanList(Class<T> clazz, String sql, Object ... param) {

        Connection connection = JDBCUtil.getConnection();

        List<T> beanList = null;

        try {
            beanList = queryRunner.query(connection, sql, new BeanListHandler<>(clazz), param);
        } catch (SQLException e) {
            e.printStackTrace();
            throw new RuntimeException(e);
        } finally {
            
            // 关闭数据库连接
            JDBCUtil.releaseConnection(connection);
            
        }

        return beanList;
    }
}
```

## 4.搭建表述层所需环境

本质上就是Thymeleaf所需要的环境

### ①导入jar包

> attoparser-2.0.5.RELEASE.jar 
>
> javassist-3.20.0-GA.jar
>
> log4j-1.2.15.jar 
>
> ognl-3.1.26.jar 
>
> slf4j-api-1.7.25.jar 
>
> slf4j-log4j12-1.7.25.jar 
>
> thymeleaf-3.0.12.RELEASE.jar 
>
> unbescape-1.1.6.RELEASE.jar

### ②创建ViewBaseServlet

```java
import org.thymeleaf.TemplateEngine;
import org.thymeleaf.context.WebContext;
import org.thymeleaf.templatemode.TemplateMode;
import org.thymeleaf.templateresolver.ServletContextTemplateResolver;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ViewBaseServlet extends HttpServlet {

    private TemplateEngine templateEngine;

    @Override
    public void init() throws ServletException {

        // 1.获取ServletContext对象
        ServletContext servletContext = this.getServletContext();

        // 2.创建Thymeleaf解析器对象
        ServletContextTemplateResolver templateResolver = new ServletContextTemplateResolver(servletContext);

        // 3.给解析器对象设置参数
        // ①HTML是默认模式，明确设置是为了代码更容易理解
        templateResolver.setTemplateMode(TemplateMode.HTML);

        // ②设置前缀
        String viewPrefix = servletContext.getInitParameter("view-prefix");

        templateResolver.setPrefix(viewPrefix);

        // ③设置后缀
        String viewSuffix = servletContext.getInitParameter("view-suffix");

        templateResolver.setSuffix(viewSuffix);

        // ④设置缓存过期时间（毫秒）
        templateResolver.setCacheTTLMs(60000L);

        // ⑤设置是否缓存
        templateResolver.setCacheable(true);

        // ⑥设置服务器端编码方式
        templateResolver.setCharacterEncoding("utf-8");

        // 4.创建模板引擎对象
        templateEngine = new TemplateEngine();

        // 5.给模板引擎对象设置模板解析器
        templateEngine.setTemplateResolver(templateResolver);

    }

    protected void processTemplate(String templateName, HttpServletRequest req, HttpServletResponse resp) throws IOException {
        // 1.设置响应体内容类型和字符集
        resp.setContentType("text/html;charset=UTF-8");

        // 2.创建WebContext对象
        WebContext webContext = new WebContext(req, resp, getServletContext());

        // 3.处理模板数据
        templateEngine.process(templateName, webContext, resp.getWriter());
    }
}
```

### ③配置web.xml

```xml
<!-- 在上下文参数中配置视图前缀和视图后缀 -->
<context-param>
    <param-name>view-prefix</param-name>
    <param-value>/WEB-INF/view/</param-value>
</context-param>
<context-param>
    <param-name>view-suffix</param-name>
    <param-value>.html</param-value>
</context-param>
```

### ④创建view目录

![./images](data:image/png;base64,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)

## 5.功能清单

- 显示首页：浏览器通过index.html访问首页Servlet，然后再解析对应的模板视图
- 显示列表：在首页点击超链接，跳转到目标页面把所有士兵的信息列表显示出来
- 删除信息：在列表上点击删除超链接，执行信息的删除操作
- 新增信息：
  - 在列表页面点击超链接跳转到新增士兵信息的表单页面
  - 在新增信息的表单页面点击提交按钮执行保存
- 更新信息：
  - 在列表上点击更新超链接，跳转到更新士兵信息的表单页面：表单回显
  - 在更新信息的表单页面点击提交按钮执行更新

## 6.显示首页

### 目标

浏览器访问index.html，通过首页Servlet，渲染视图，显示首页。

### 思路

![./images](data:image/png;base64,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)

### 代码

#### 创建PortalServlet

> PortalServlet.java

```java
@WebServlet("/index.html")
public class PortalServlet extends ViewBaseServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        String viewName = "portal";

        super.processTemplate(viewName, request, response);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    }
}
```

#### 创建portal.html

![./images](data:image/png;base64,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)

> portal.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>士兵信息管理系统</title>
</head>
<body>

    <a th:href="@{/SoldierServlet?method=showList}">显示士兵信息列表</a>

</body>
</html>
```

## 7.显示列表

### 目标

在目标页面显示所有士兵信息，士兵信息是从数据库查询出来的

### 思路

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img031.5451e78a.png)

### 代码

#### Soldier

> Soldier.java

```java
public class Soldier {
    private Integer soldier_id;
    private String soldier_name;
    private String soldier_weapon;

    public Soldier() {
    }

    public Soldier(Integer soldier_id, String soldier_name, String soldier_weapon) {
        this.soldier_id = soldier_id;
        this.soldier_name = soldier_name;
        this.soldier_weapon = soldier_weapon;
    }

    public Integer getSoldier_id() {
        return soldier_id;
    }

    public void setSoldier_id(Integer soldier_id) {
        this.soldier_id = soldier_id;
    }

    public String getSoldier_name() {
        return soldier_name;
    }

    public void setSoldier_name(String soldier_name) {
        this.soldier_name = soldier_name;
    }

    public String getSoldier_weapon() {
        return soldier_weapon;
    }

    public void setSoldier_weapon(String soldier_weapon) {
        this.soldier_weapon = soldier_weapon;
    }

    @Override
    public String toString() {
        return "Soldier{" +
                "soldier_id=" + soldier_id +
                ", soldier_name='" + soldier_name + '\'' +
                ", soldier_weapon='" + soldier_weapon + '\'' +
                '}';
    }
}
```

#### ModelBaseServlet

创建这个基类的原因是：我们希望每一个模块能够对应同一个Servlet，这个模块所需要调用的所有方法都集中在同一个Servlet中。如果没有这个ModelBaseServlet基类，我们doGet()、doPost()方法可以用来处理请求，这样一来，每一个方法都需要专门创建一个Servlet（就好比咱们之前的LoginServlet、RegisterServlet其实都应该合并为UserServlet）。

> ModelBaseServlet.java

```java
public class ModelBaseServlet extends ViewBaseServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        // 在doGet()方法中调用doPost()方法，这样就可以在doPost()方法中集中处理所有请求
        doPost(request, response);
    }
    
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        // 1.从请求参数中获取method对应的数据
        String method = request.getParameter("method");

        // 2.通过反射调用method对应的方法
        // ①获取Class对象
        Class<? extends ModelBaseServlet> clazz = this.getClass();

        try {
            // ②获取method对应的Method对象
            Method methodObject = clazz.getDeclaredMethod(method, HttpServletRequest.class, HttpServletResponse.class);

            // ③打开访问权限
            methodObject.setAccessible(true);

            // ④通过Method对象调用目标方法
            methodObject.invoke(this, request, response);
        } catch (Exception e) {
            e.printStackTrace();

            throw new RuntimeException(e);
        }
    }

}
```

#### SoldierDao.selectSoldierList()

![./images](data:image/png;base64,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)

![./images](data:image/png;base64,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)

接口方法：

> SoldierDao.java

```java
public interface SoldierDao {

    List<Soldier> selectSoldierList();

}
```

实现类方法：

> SoldierDaoImpl.java

```java
public class SoldierDaoImpl extends BaseDao<Soldier> implements SoldierDao {
    @Override
    public List<Soldier> selectSoldierList() {
        
        String sql = "select soldier_id soldierId,soldier_name soldierName,soldier_weapon soldierWeapon from t_soldier";
        
        return getBeanList(Soldier.class, sql);
    }
}
```

#### SoldierService.getSoldierList()

![./images](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQEAAADVCAIAAADYVtInAAASRklEQVR42u2dbWwcxRnH5+zEccxLQgi2oMbGwZdYIU6qfigxEFXIoVGcVEpF0i8lBAnZriMVxW4VKbRRjFBBisAOqohrRxV1A59CVVAdnxLFQBtICh/aUkfIyZkghwC1C9S8OeHAdvf2dXZ39vZub+92duf/+wB7ezuzu77nNzuz2WcnNj8/TwAQmBgcAIIDB4DowAEgOnAAiI7VgT+f/Ku+XFG+aNWK2tuqbw76IHMi0R5rGSBtw/P9mwtSdVPPhTOd8aDPEvhHJgcUVsfrVtXVFPYokr13rew6qyzLMUaoFYRan0XswQGQG+4OOPHjH/7Ap2MwopbIS9YoUwwpSFR7OFA4EDX8cECJ0aae4R3HWuTGWw0TLXaHSUvLgBLCSrgraEFNR5ZWFR1mTpFnavC1gufPNDxtug4Ye5SrGKcro2uQl1me6dco9UT0I7HUTB38/rGV6W+MHRLTZYz1RwDB4Z8Dpi+pDk1TU9PZs2dJ2/H5bS8bv71COgLqTa28rSeToWtDy2Esj1sD27y/bS/phdRvjWMlTqLZTi3OqFk9E/V8lW2pZYeC0CBwfHRA/S0Ten9m65C83tzq2j4Nkl3ODrCuCwaWwKeDTK6BriypBrmxu3TIHiNSkDaqvbBRJwVoz4hNNK1m7XzltVq7QH+w9/YSzL4fKC5+9oWUX9L4pMSEFs+WcNY/MhywbGQ0lHojqmyhf/3LMaMVNwK/3n59ordteCr2eENPY1fXqHIQx3aY2mnjDJzOjFnz2SbrYWymzDZt4qY4KA7ZOpBpBGy6DlAfzL0cSxNvGQhbhhC0Nhn6CuoGPT2jXV2Ntorr2RGmtttS9B9rkE2QLgBpFYh9P5mvcOyxe0YH1OuAY88PBEAODtybmLCsfHVzbfp/SWZ7q3UBGK24eTMqttIBacREFq2kEs9NaofGppplj/T4OV2ocb8qivZhM7N+1j1aVs3ZOLAZ4wHu8M+BJrkxpW+BMJpxh1sizNXmRtgBU7+bqsvskaVqpwsXczcJ/caOct/LfHZ0zVk5QHBfiDf8dAC9WhBGcnheCA6ASAIHgOj44QAAYQbPTgPRgQNAdOAAEB04AEQHDgDRgQNAdOAAEB0/HXj63Cf68nULS9bftHjtsvKgTxAAFwrlgMLdVRWSCUGfIwCZKKwDTvxizY1BnzgAKlYH9uzZs3Tp0o6OjqqqKmXN5ORkX1/f9PT0oUOHMtcFB0AYsTrQ3d0thXtFRUV7e3ttbe3ExER/f//MzIwkhvRV5rq8OUA9h2880D+2n36Hg+0NDgD4h9UBSYDDhw9PTU2VlZVt3Ljx1KlTqVSqsrJy9+7dkgaZ6/LigBLwpjySpD0FcxShDwoGYzwgtfqSBpcvX1Y+VldXSwJIVwbXujxdB+yvVjBrIX3/eAMMAIWDPSaW2v4jR44kk8l4PN7a2ipdE7KpK4/xAJ2CAAdAUXG8LzQ3NzcyMtLc3FxSUpJlXd76Qr3jnZ1akq8c+pbuUfpCob3yIdHbW98JHYCvBH9v1BjwUq99MA0RjFEzMtCB/wTvAADBgueFgOjAASA6cACIDhwAogMHgOjAASA6cACIDhwAogMHgOjAASA6vDhAz3tQUb5o1Yra26pvDvqg8ib9pJMyzZkfteER2sLAowMKq+N1q+pqgj6u/IADYYBfB5zINDtgoWBkuwUAHCgMfjqQTz4+HHAHDhQGPx3IJx9fd6C0pOTWm9MKvf/R5OzcnH1LswP2dHvmjHdy+Chz6hFqjlRmkr41yZ+q0Jrj36TN8GrOfmOnA2VdynQ05nksjcNlnrjrOWI6QAZ+OpBPPr7uwJ3fveOWyuXSwoeT/33z7XfsW1IO2NPtzWuMFLQEcx57dkZ/+9DWfrm8UZzejs5r06eod3Ugl1LGwdCl6HOjrwh6MddzdPrjiI7P4wHP+fi6Az9qvmdBaam08O3s7F9GXrdvaThg7xtY19DxoX/htGzg8LoXbZpVuoT+MbMDOZVyOh39o22OYznyx13Ocdzpj+Pj7x9K/B8Te8vHN64D61bfUnUTyeY6kJUDu8igEjXZOUC10VSQ8OcAw1y3cxx3+uP4+/uHj4LcF/KQj687UJIeD1SS9Hhgas5lPGBPtx+3Xu7VX90tPoh2E5MKFFmHxlz6QuptUKNgVn0hZillpUMpax+pnfQru8jsecLhjyM6Ib83yki3dx4TZ+NA3Kixqa2NDJD9ep6/tNZ4+Yu6iTG6pY7FKGht5rMvpf2rAj30pUrZu2vu5xgnGBMzCbkDgeOtNUUbzBO8OBAepBb4qYYzub4H0lspUAzgQO5Q/ZAc3gHsrRQoPHAAiA4cAKIDB4DowAEgOnAAiA4cAKIDB4DowAEgOlFwwId8fDy8IDAcOaCkYir/zamgD/n4cEBgOHJAScWsrKyUNMgm7UbHh+ft4IDAcOTA5OTkM888MzMzU11d/cgjj2SZfEPgAMgPjhyQmJiYePbZZ1OpVDwe7+joyDIFJ/98/DT6g2yMR/MJnryPMHw5IHHy5Mnh4WFpYcuWLffdd182RTzn47PS1Zk59chGjzJ8OZDndcB7Pr75I+PtKshGjy4cOZD/eMB7Pr4pyd2WU59ANnqU4ciB/O8Lec3HpwI/wcypRzZ6lOHIAR//fcAJ05iYna7OzqnHmDjCcOSAZ8Kajw/4IAoOAJAPcACIDhwAogMHgOjAASA6cACIDhwAogMHgOjAASA6cACIThQcKN4c9/7OuQ34gCMHgsypzxI4EEU4ciDInPpMMDNmkEYTHThyIMic+kzAgYjDkQMkuJx601TvPY1dXfr07uP0JPXnB8lDK8d+Pb/tZX3l+n37Yk++tgPpNSGGLwdIUXPqHaZ6N6blNmaqHDOmp8w0Y7G0+NI2XBxCBl8OFDWn3mWqdz1p2M0B0wTAUCB8cORAkDn1jLXZO6BuOkh2YYgQRjhyILiceuZU7zk4IG871khGG/CyiRDCkQPFzql3merdeIGKPkm9MiZmzFyPOYfDDEcOeIaHnHrcEAovUXAgePCvBWEGDuSLcocJrxwKL3AAiA4cAKIDB4DowAEgOnAAiA4cAKIDB4DowAEgOlFwoHg59XaQYRx+ouaAQqFy6u3AgfATTQecwDw0wA4vDiiPTHd0dFRVVSlrJicn+/r6pqenDx06lLksHAD5wIsDSgJNRUVFe3t7bW3txMREf3//zMyMJIb0Veay3nLqWdPR27PslSdCh0lLy4A5fV7pBNEZBQ5J+pY1gDt4cUAS4PDhw1NTU2VlZRs3bjx16lQqlaqsrNy9e7drSo2XnHrG087MLHvFFHuOjbZBvV6PPYuGWWHQf2hggxcHJKRWX9Lg8uXLysfq6mpJgGySKr3k1KstNNU6s7PsiTl2tbAmtCPMebydKsSlgDs4ckBCavuPHDmSTCbj8Xhra2uWafVecupVlGbe9k4J8wZ0+62E+iDZReVZOjuA1LIwwJcDEnNzcyMjI83NzVm+WIV4y6lP9vaOd3Zqk9TrLxeyZdnb+jCW9PmkqS+kFU/09tZ3yu/nslUIuIM7Bzzg7b6Q0VXRh8SMYbK9Hy9v1EgX0b43itOlreNuwBviOgCAQhQcACAf4AAQHTgARAcOANGBA0B04AAQHTgARAcOANGBA0B04AAQHdEdKHg+PhKOuQcOFDgfHw5wDxzA83aiEwUHkI8P8iEKDhQ/H98500DOvqfXI5GYe6LgQLHz8aW4bh/a2i/38I3sMVv2vbIeDnBPFBwgxc7HT2O7EliC3f7iCcApEXGAFDMfXw5/0mN6xwocCC/RcYAULR+femEElVxsyjM2PqAvxD2RcsADnu4LGf2gprY2MkCM60Bj28CAOVEfDnAPHPDr3iiCPayI7oB/wIGwAgf8Ag6EFTgARAcOANGBA0B0YufOnQv6GAAIEjgARAcOANGBA0B04IAPfDP/9aWrFz5OfTgz96X0saLk2uVlt9SUr1wYWxT0oQF34EC+TH79/jtfvTVLvrWsLyULVl/z/apFt3queX7+9GONI82jBzbEYqb1p7sbf7fi+PM7ay4dfWDLiU3Hn3+wNuZ1J54ObOKPgey3QMCBvJAEODdz1un+ciwWW1PRZNFAjuyOF+Xl7X2j3Rscw8h3B7LftUs9cAAopOauvjF93H4FoJGuBncv3VJWUq58VKKQyPE3Pz9x9IHn6p63hriOqwO1sRxCMKddCwUc8M67V0bfu2Jk2wz1vqovb+28V1+uW7z69sWNynK6BX2UPJFd+PrsQC67Fgo44J03Pzvxxew0vebfp8ak/67d2ECvvK506Z1LNinLdGNMb0P3UuR+SjruaQfMGxCybq/WF7r4M9sG0pcvPFgrN/bS132ko+PFdXuHjtb9Ya3LrhkF17a2xo68tSm9Xtpg4o8/lTpBQ7+Z/9XW95z3a10T9A/lAhzwzquf/snSEWI6IHWH7l12v/4x3YqnI0QNdKJFYVILF3kDKVYP3ENeVxyQF4zwPd29Jr015YC8QfrSIHXQtQiW1qa/Pvg2tSP2rl0KGsMPou2vht6vceROFXoeeBQHOOAdbw4opBvUg29L0Xiue4Olb0PFouaAGuHaBqYxsbYhdZEg6nWCMEPQumu3gnpYa6sVR7T9mntlzAo5vxTAAe946AvR6P2iA+QxmwNyz70mFwdsI4QMzbDTrp0KSlceaasnyKPSYaV7O+n7Qs4O5D5WCRY44B2PY+Ln6l7o3kDo9rXmdWtfSO17MPpCSoAeJPa+EN1Z6iYHpJWXTM25864zF1TLPnoxTpIrnpA7OboDpgM7ffRozc6dl+wVcn73CQ54x8O9UaJ3RWT0m/TuY2Kjj7Fu7974wRMrrGPidFyq9W6nbKFDmb3rLAqq4sXT3SetiH2/2mHbKgz6h3IBDuSFh38jA7wBB/KlcM9KgOIAB3wAz8yFGjgARAcOANGBA0B08F4JIDpwAIgOHACiAweA6MABIDqiO+Blnnofpt1OtMde2oZ3VPMBHMh9nno4EC3gQCBzdMMBjoiCAyGcpx4OcEQUHCj2PPXGjDPyDJXDO461pGfoS8/CR9pj8jT1TT3GvJWMyevhAE9EwYFiz1NvcqBlQIl3edE2XbfD5PVwgCei4AAp8jz1luuAOjhmLjtM3L0ZDnBERBwgxZ6nHg5Eh+g4QIo2T32ODjAmr0dfiCci5YAHvNwXyvU6YJ+8Hg7wBBwo6L1RTFocAkR3oMDAgRAABwoKHAgBcACIDhwAogMHgOjAASA6cACIDhwAogMHgOjAAR+4Mjv/j0+uXPz8m/+lZqWPN5SVrrh+4fduXLy4lPdX7wMCB/LnwmepEx98mZqz/hnLSmKbvnPtyiVZPb7qgMNjRabHkfLMbPZEMPst1ENWcCAvJAGGLn/h9CeMxcjW6utsGiTUZDPqGToHfHcg+11nJHcH6CcKvQIH+GPm27nfX5i2XwFopKvBwyuXVizQn+U2csnkUHqq4UyGH9XNgdyON6dd+wwciCZvTM38feqKsjw3N/vu306+/883U199vqzm9jtatl+zXE3wX1+5+O5KLaNNir1dZDDbWPDVgdx27TNwIJocHf9s6qo6BdP5V45/OfXRHVu2L1hU/vHFC5IGZRXXKF9Vli/YWb9EK0Q3xjRGL8UhzYDeQEvaNz2SZ2zAyOhv6jl/puFpt10zCq7fty/25Gtav0fpBJ0fJA9l2q99De0Ady8igAPe+e07n+odoVd6D9z1cGf59YwUfqk79PPVy4zPaoTQHfL0qlEtXFip9yZzjK3Z2Tz6WnNGv+Ou3Qoam2gb1JveKmAcuWOFFgf4ehEBHPCOzYE95dffYN/M6oCM8jurP7+1o2BLO7ZsYE9XNl8kiNqmEuaT29ZduxfU9kdoR7T9Wro47Arj1usAT0nYcMA75r7Q0Bf/+WDN1p+ULlw0eX702hsrl95ap3xl7gvRaE0csTug9NxzcYDR3c6QveC0a3ZBpfpBsksdUGR2gNXxhwPRxDImTr6W+OBfb31z9cryFStXb75/8RK17beOiY37MfqvbusLqYHB7AvJ7Tix94XozlI76Td1LzLv2qWgUnbXWCMZbRikeuzW/SZ6e+s7O8dZFebsQDFfRAAHvOPp3qjWFZGxd9XNq6lfnR5n9jR2HbO1mFS9bVT80KHM3nUWBU2haPneKE6XtlSY+3WgiC8igAN54enfyEBmip2ACgfypZDPSogJHAgheGbOV+AAAMUFDgDRgQNAdOAAEB04AEQHDgDR+T8Weo8bzZE3KgAAAABJRU5ErkJggg==)

接口方法：

> SoldierService.java

```java
public interface SoldierService {

    List<Soldier> getSoldierList();

}
```

实现类方法：

> SoldierServiceImpl.java

```java
public class SoldierServiceImpl implements SoldierService {

    private SoldierDao soldierDao = new SoldierDaoImpl();

    @Override
    public List<Soldier> getSoldierList() {

        List<Soldier> soldierList = soldierDao.selectSoldierList();

        return soldierList;
    }
}
```

#### SoldierServlet.showList()

> SoldierServlet.java

```java
protected void showList(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    // 1.调用Service方法获取集合数据
    List<Soldier> soldierList = SoldierServiceImpl.getSoldierList();

    // 2.将集合数据存入请求域
    request.setAttribute("soldierList", soldierList);

    // 3.渲染视图（在渲染的过程中，已经包含了转发）
    processTemplate("list", request, response);
}
```

## 8.删除功能

### 目标

点击页面上的超链接，把数据库表中的记录删除。

### 思路

#### 先不考虑后续

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img035.a261c850.png)

#### 加上后续返回响应页面

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img038.be79442a.png)

### 代码

#### 完成删除超链接

![./images](data:image/png;base64,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)

```html
<a th:href="@{/SoldierServlet(soldierId=${soldier.soldierId},method='remove')}">删除</a>
```

关于@{地址}附加请求参数的语法格式：

- 只有一个请求参数：@{地址(请求参数名=普通字符串)}或@{地址(请求参数名=${需要解析的表达式})}
- 多个请求参数：@{地址(名=值,名=值)}

官方文档中的说明如下：

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img037.78b02342.png)

#### Servlet方法

```java
protected void remove(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    // 1.从请求参数中获取士兵信息的id值
    String soldierId = request.getParameter("soldierId");

    // 2.调用Service方法执行删除操作
    soldierService.remove(soldierId);

    // 3.后续……
    // 方案一：还是直接前往list.html，需要重新查询soldierList数据，代码重复
    // 1.调用Service方法获取集合数据
    // List<Soldier> soldierList = soldierService.getSoldierList();

    // 2.将集合数据存入请求域
    // request.setAttribute("soldierList", soldierList);

    // processTemplate("list", request, response);

    // 方案二：直接调用隔壁的showList()
    // 也能实现需求，但是总感觉这样调用方法破坏了程序的结构
    // showList(request, response);

    // 方案三：通过请求转发的方式间接调用showList()方法
    // request.getRequestDispatcher("/SoldierServlet?method=showList").forward(request, response);

    // 方案四：通过请求重定向的方式间接调用showList()方法
    response.sendRedirect(request.getContextPath() + "/SoldierServlet?method=showList");
}
```

#### Service方法

```java
    @Override
    public void remove(String soldierId) {
        soldierDao.delete(soldierId);
    }
```

#### Dao方法

```java
    @Override
    public void delete(String soldierId) {
        String sql = "delete from t_soldier where soldier_id=?";

        update(sql, soldierId);
    }
```

## 9.前往新增信息的表单页面

### ①创建超链接

```html
<a th:href="@{/SoldierServlet?method=toAddPage}">前往新增页面</a>
```

### ②Servlet

```java
protected void toAddPage(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    processTemplate("add-page", request, response);
}
```

### ③创建表单页面

![./images](data:image/png;base64,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)

```html
<form th:action="@{/SoldierServlet}" method="post">

    <input type="hidden" name="method" value="saveSoldier" />

    士兵姓名：<input type="text" name="soldierName" /><br/>
    士兵武器：<input type="text" name="soldierWeapon" /><br/>

    <button type="submit">保存</button>

</form>
```

## 10.执行保存

### ①目标

提交表单后，将表单数据封装为Soldier对象，然后将Soldier对象保存到数据库。

### ②思路

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img040.f6306887.png)

### ③代码

#### [1]Servlet方法

```java
protected void saveSoldier(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    
    // 1.获取请求参数
    String soldierName = request.getParameter("soldierName");
    String soldierWeapon = request.getParameter("soldierWeapon");
    
    // 2.创建Soldier对象
    Soldier soldier = new Soldier(null, soldierName, soldierWeapon);

    // 3.调用Service方法
    soldierService.saveSoldier(soldier);

    // 4.重定向请求
    response.sendRedirect(request.getContextPath() + "/SoldierServlet?method=showList");
}
```

#### [2]Service方法

```java
    @Override
    public void saveSoldier(Soldier soldier) {

        soldierDao.insertSoldier(soldier);

    }
```

#### [3]Dao方法

```java
    @Override
    public void insertSoldier(Soldier soldier) {

        String sql = "insert into t_soldier(soldier_name,soldier_weapon) values(?,?)";

        update(sql, soldier.getSoldierName(), soldier.getSoldierWeapon());
    }
```

## 11.前往修改信息的表单页面

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img041.f3383f21.png)

### ①创建超链接

```html
<a th:href="@{/SoldierServlet(soldierId=${soldier.soldierId},method=toEditPage)}">编辑</a>
```

### ②Servlet方法

```java
protected void toEditPage(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    // 1.从请求参数获取soldierId
    String soldierId = request.getParameter("soldierId");

    // 2.根据soldierId查询Soldier对象
    Soldier soldier = soldierService.getSoldierById(soldierId);

    // 3.将Soldier对象存入请求域
    request.setAttribute("soldier", soldier);

    // 4.前往更新的表单页面
    processTemplate("edit-page", request, response);

}
```

### ③Service方法

```java
    @Override
    public Soldier getSoldierById(String soldierId) {
        return soldierDao.selectSoldierByPrimaryKey(soldierId);
    }
```

### ④Dao方法

```java
@Override
public Soldier selectSoldierByPrimaryKey(String soldierId) {
    String sql = "select soldier_id soldierId,soldier_name soldierName,soldier_weapon soldierWeapon from t_soldier where soldier_id=?";

    return getBean(Soldier.class, sql, soldierId);
}
```

### ⑤表单页面

```html
<form th:action="@{/SoldierServlet}" method="post">

    <input type="hidden" name="method" value="updateSoldier" />
    <input type="hidden" name="soldierId" th:value="${soldier.soldierId}" />

    士兵姓名：<input type="text" name="soldierName" th:value="${soldier.soldierName}" /><br/>
    士兵武器：<input type="text" name="soldierWeapon" th:value="${soldier.soldierWeapon}" /><br/>

    <button type="submit">更新</button>

</form>
```

## 12.执行更新

![./images](https://heavy_code_industry.gitee.io/code_heavy_industry/assets/img/img042.f3aaae74.png)

### ①Servlet方法

```java
protected void updateSoldier(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    // 1.获取请求参数
    String soldierIdOrigin = request.getParameter("soldierId");
    Integer soldierId = Integer.parseInt(soldierIdOrigin);
    String soldierName = request.getParameter("soldierName");
    String soldierWeapon = request.getParameter("soldierWeapon");

    // 2.封装对象
    Soldier soldier = new Soldier(soldierId, soldierName, soldierWeapon);

    // 3.调用Service方法执行更新
    soldierService.updateSoldier(soldier);

    // 4.重定向请求
    response.sendRedirect(request.getContextPath() + "/SoldierServlet?method=showList");
}
```

### ②Service方法

```java
    @Override
    public void updateSoldier(Soldier soldier) {

        soldierDao.updateSoldier(soldier);

    }
```

### ③Dao方法

```java
@Override
public void updateSoldier(Soldier soldier) {
    String sql = "update t_soldier set soldier_name=?,soldier_weapon=? where soldier_id=?";
    update(sql, soldier.getSoldierName(), soldier.getSoldierWeapon(), soldier.getSoldierId());
}
```

## 13.请求字符集设置

- 设置请求体字符集需要调用`request.setCharacterEncoding("UTF-8");`
- `request.setCharacterEncoding("UTF-8");`要求在所有`request.getParameter()`前面
- 在执行子类Servlet方法时，其实都是先调用父类ModelBaseServlet的doPost()方法
- doPost()方法中包含获取method请求参数的操作
- 所以最前面的`request.getParameter()`在doPost()方法中
- 所以`request.setCharacterEncoding("UTF-8");`要放在doPost()方法的`request.getParameter()`前面

```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    // 0.在所有request.getParameter()前面设置解析请求体的字符集
    request.setCharacterEncoding("UTF-8");

    // 1.从请求参数中获取method对应的数据
    String method = request.getParameter("method");
    
    // ……
```