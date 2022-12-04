# 创建Java Web工程并运行

**注意**：在2022版本中的IDEA中，无法直接创建Java Web工程。旧版本中可直接新建Java Web项目。下列操作可忽略。

1. 首先，创建一个[普通的Java工程](create_java.md)

2. 单击项目，右键添加框架支持(Add Framework Support...)，选中web Application，选择Create web.xml，即可。

   ![4](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302009777.gif)

# 配置Tomcat

**注意**：在配置Tomcat之前，需要保证安装并配置了Tomcat的环境变量，如果没有安装，请先安装并配置成功。

在命令行输入：`catalina run` 。能够启动tomcat，则证明安装配置成功。

**设置IDEA**：

1. **进入设置**：点击File --> settings：

   ![image-20221130203027866](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302034708.png)

2. 点击Build,Execution,Deployment --> Application Servers

   ![image-20221130203102451](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302034253.png)

3. 添加Tomcat server

   ![image-20221130203255059](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302034854.png)

4. 选中Tomcat目录：

   ![image-20221130203318880](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302034394.png)

5. Apply、OK即可。

![5](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302034193.gif)

------

**配置Tomcat**：

1. ![image-20221130203944209](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302045625.png)
2. ![image-20221130204106011](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302045114.png)
3. ![image-20221130204159071](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302045719.png)
4. ![image-20221130210255826](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302102519.png)
5. ![image-20221130204331618](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302045011.png)
6. ![image-20221130210403489](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302104146.png)

![6](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302044133.gif)

## 乱码问题

如果Tomcat日志出现乱码，需要配置： 

![image-20221130204907919](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302056751.png)

**解决方案**： 

1. 点击Help --> Edit custom VM Options，在最后面添加

   ```shell
   -Dfile.encoding=UTF-8
   ```

   ![image-20221130205032187](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302050793.png)

2. 在当前Tomcat实例中配置 VM option，添加 

   ```shell
   -Dfile.encoding=UTF-8
   ```

   ![image-20221130205248786](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302052039.png)

3. 在第二步的Startup/Connection页签的Run和Debug添加一个key为 `JAVA_TOOL_OPTIONS` ， value为"`- Dfile.encoding=UTF-8`"的环境变量 

   ![image-20221130205553985](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211302055152.png)

4. 保存后重启IDEA，可以发现控制台中文乱码显示正常了。

