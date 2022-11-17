# 创建项目

## 通过Spring脚手架创建(推荐)

1. 访问https://start.spring.io/

   ![image-20220826215407623](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160837628.png)

2. 将生成的压缩包解压，查看生成的gradle 项目目录结构如下所示:

   ![img](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160837724.jpeg)

**注意**：

- 当对Java源码生成对应的class文件，之后才会生成build目录

- 可以删掉一些不必要的文件：

  ![image-20220826220055095](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160840039.png)

## 通过命令行创建

1. 创建一个文件夹，并启动cmd

   ![image-20220827083554832](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160840697.png)

2. 使用 `gradle init`初始化项目

   ![image-20220827083632065](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160840754.png)

3. **选择要生成的项目类型**：选择`2`选择生成一个应用

   **选择实现语言**：选择 `Java`

   **是否跨多个子项目拆分功能**：选择`1`单应用项目，`2`为多模块项目

   **选择构建脚本**：选择`Groovy`

   **使用新的api和行为生成构建**：`no`

   **使用测试框架**：选择`JUint4`

   **制定项目名**：不指定默认选择所在文件名

   **制定源码包的目录**：通常使用公司域名的反写

   ![image-20220827084613240](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211160840813.png)

**说明**：src目录、build.gradle放在了app目录中。

# IDEA创建由Gradle管理的项目

## 创建普通Java工程

**注**：本版本基于IntelliJ IDEA 2022.2.1，在旧版本中可以直接构建Gradle项目

1. 创建由Gradle管理的项目：

   ![image-20220904205501215](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211170841217.png)

2. 修改当前项目使用的本地安装的Gradle(可以加快下载项目依赖jar包的速度)：

   点击文件-设置-构建、执行、部署中的Gradle选项

   ![image-20220904211233273](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202211170841869.png)

   - Gradle用户主目录就是设置gradle的本地缓存的，将它设置`GRADLE_USER_HOME`所在目录即可。
   - 不使用gradle-wrapper文件中的Gradle，选中本地指定位置的Gradle
   - 选择本地的JVM文件
   - 点击应用、确定即可

   这样下载依赖的时候 ，就会在本地安装的Gradle环境下构建。

当用IDEA创建gradle项目后，每次使用的都是idea插件里面的指定版本的wapper(IDEA安装目录\plugins\gradle\lib中后缀所展示的版本)

![image-20220904210524188](./assets/image-20220904210524188.png)

下载的依赖放在了`GRADLE_USER_HOME\caches\modules-2\files-2.1`中：(文件-项目结构中查看 快捷键 `Ctrl+Alt+Shift+S`)

![image-20220904212813247](./assets/image-20220904212813247.png)

图形化界面使用的就是本地的Gradle版本，而gradlew用的就是IDEA中gradle wrapper中的版本，两者可能不一致。

![image-20220904210550033](./assets/image-20220904210550033.png)

以后就可以在src-main-java中写代码了，在resources中写对应的业务逻辑配置文件，在test中写测试代码及所对应的业务逻辑配置文件。

![image-20220904214048439](./assets/image-20220904214048439.png)

**注意**：每次创建项目都要重新设置一下本地Gradle

## 创建web工程

**注**：本版本基于IntelliJ IDEA 2022.2.1

在idea 新版本的创建项目中，无法自己选择创建项目是普通Java工程还是web工程了(IDEA 旧版本是可以的)。

如果想创建 web 工程，只需要创建普通Java工程后在 `src/main/`目录下添加`webapp/WEB-INF/web.xml` 及页面即可。

**步骤**：

1. **第一步**：导入对应的依赖信息
2. **第二步**：编写对应的配置文件
3. **第三步**：编写业务逻辑代码
4. **第四步**：进行部署

**例**：

1. 在build.gradle中添加war依赖信息：

   ![image-20220906083730979](./assets/image-20220906083730979.png)

2. 导入对应的依赖信息，并重新加载项目，此时会将对应的依赖信息下载到本地缓存(下载路径见[创建普通Java工程](#创建普通Java工程))：

   ```groovy
   implementation 'org.springframework:spring-beans:4.1.7.RELEASE'
       implementation 'org.springframework:spring-web:4.1.7.RELEASE'
       implementation 'org.springframework:spring-webmvc:4.1.7.RELEASE'
       implementation 'org.springframework:spring-tx:4.1.7.RELEASE'
       implementation 'org.springframework:spring-test:4.0.5.RELEASE'
       implementation 'org.springframework:spring-jdbc:4.1.7.RELEASE'
   
       implementation 'org.mybatis:mybatis-spring:1.2.3'
       implementation 'org.mybatis:mybatis:3.3.0'
   
       implementation 'mysql:mysql-connector-java:5.1.36'
       implementation 'com.alibaba:druid:1.0.15'
   
       implementation "com.fasterxml.jackson.core:jackson-databind:2.2.3"
       implementation "com.fasterxml.jackson.core:jackson-annotations:2.2.3"
       implementation "com.fasterxml.jackson.core:jackson-core:2.2.3"
   
       implementation 'org.aspectj:aspectjweaver:1.8.6'
       implementation 'log4j:log4j:1.2.17'
       implementation 'org.slf4j:slf4j-api:1.7.25'
       implementation 'jstl:jstl:1.2'
       compileOnly 'javax.servlet:servlet-api:2.5'
       testImplementation group: 'junit' ,name: 'junit', version: '4.12'
   ```

   ![image-20220906084641368](./assets/image-20220906084641368.png)

3. 在main目录中添加`webapp`目录，在webapp中创建`WEB-INF`，将[web.xml](Demo/web.xml)放入到`WEB-INF`

   ![image-20220906090024857](./assets/image-20220906090024857.png)

   将对应的业务逻辑代码所需要的配置文件放入到resources中：

   [applicationContext.xml](demo/applicationContext.xml)、[jdbc.properties](demo/jdbc.properties)、[mybatis-config.xml](demo/mybatis-config.xml)、[springmvc.xml](demo/springmvc.xml)

   ![image-20220906090504938](./assets/image-20220906090504938.png)

4. 将[业务逻辑代码](demo/com)复制到java文件中：

   ![image-20220906095200744](./assets/image-20220906095200744.png)

   将[Mapper接口的映射文件](demo/AdminMapper.xml)放在resources中：

   ![image-20220906095114369](./assets/image-20220906095114369.png)

## 项目部署

### 部署到本地Tomcat

![image-20220906102435419](./assets/image-20220906102435419.png)

### 使用Gretty插件部署

