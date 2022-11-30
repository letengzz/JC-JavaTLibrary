# 安装目录结构

![image-20221013202507344](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232011123.png)

其中，在bin目录下：

![image-20221013203451524](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232011226.png)

在IDEA的VM配置文件中：

**说明**：64 位操作系统中 8G 内存以下的机子或是静态页面开发者是无需修改的。 64 位操作系统且内存大于 8G 的，如果你是开发大型项目、Java 项目或是 Android 项目， 建议进行修改。

- `-Xms128m`：设置初始的内存数，增加该值可以提高 Java 程序的启动速度。(16 G 内存的机器可尝试设置为 `-Xms512m`)
- `-Xmx750m`：设置最大内存数，提高该值，可以减少内存 Garage 收集的频率，提高程序性能(16 G 内存的机器可尝试设置为 `-Xmx1500m`)
- `-XX:ReservedCodeCacheSize=240m`：保留代码占用的内存容量(16G 内存的机器可尝试设置为`-XX:ReservedCodeCacheSize=500m`)

# 设置目录结构

**使用旧版本**：设置目录在 `C:\Users\{当前用户}`目录下的 `.IntellijIdea20xx.x`的目录。

![image-20221014102025037](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232011371.png)

config：

![IDEA设置目录config](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232011989.png)

system：

![IDEA设置目录system](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232011836.png)

**使用新版本**：新版本不会生成config和system目录。

**类似config的目录**：`C:\Users\{当前登录的系统用户名}\AppData\Local\JetBrains\IntelliJIdea2020.3`

**类似system的目录**：`C:\Users\{当前登录的系统用户名}\AppData\Roaming\JetBrains\IntelliJIdea2020.3`

类似config的目录就是配置目录，它里面存放的是IntelliJ IDEA相关的一些配置信息，比如模板、快捷键、插件等等，毫无疑问该目录是IntelliJ IDEA安装当中最重要的一个目录，没有之一。

类似system的目录就是系统目录，IntelliJ IDEA会将我们程序整个运行当中的一些缓存数据、索引等等生成在系统目录下的caches目录中，系统目录也是一个非常重要的目录。

------

这是 IDEA 的各种配置的保存目录。这个设置目录有一个特性，就是你删除掉整个目录之后，重新启动 IntelliJ IDEA 会再自动帮你生成一个全新的默认配置， 所以很多时候如果你把 IntelliJ IDEA 配置改坏了，没关系，删掉该目录，一切都会还原到默认。