# SpringBoot工具

## Lombok

Lombok是⼀个可以通过简单的注解形式来帮助我们简化消除⼀些必须有但显得很臃肿的 Java代码的⼯具，通过使用对应的注解，可以在编译源码的时候⽣成对应的方法。简而言之，⼀句话就是：通过简单的注解来精简代码达到消除冗⻓代码的⽬的。

- Lombok官网：https://projectlombok.org/

- GitHub地址：https://github.com/projectlombok/lombok

### Lombok优点

- 提⾼编码效率 

- 使代码更简洁 
- 消除冗⻓代码 
- 避免修改字段名字时忘记修改⽅法名

### Lombok使用

在SpringBoot中添加依赖：

```xml
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
</dependency>
```

****

在IDEA中安装Lombok插件，安装后重启即可：

![image-20230222164401161](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828921.png)

Lombok既是⼀个IDE插件，也是⼀个项⽬要依赖的jar包。Lombok是依赖jar包的原因是因为编译时要⽤它的注解。是插件的原因是他要在编译器编译时通过操作AST(抽象语法树)改变字节码生成。也就是说他可以改变java语法。他不像spring的依赖注⼊或者hibernate的orm⼀样是运⾏ 时的特性，⽽是编译时的特性。

****

重构pojo类：

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
	private String name;
	private Integer age;
}
```

简化日志开发：

```java
@Slf4j
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(@RequestParam("name") String name){
        
        log.info("请求进来了....");
        
        return "Hello, Spring Boot 2!"+"你好："+name;
    }
}
```

如果觉得@Data这个注解有点简单粗暴的话，Lombok提供⼀些更精细的注解，⽐如 @Getter、@Setter，(这两个是field注解)，@ToString，@AllArgsConstructor(这两个是类注解)。这些可能是最常见的用法,更详细的⽤法可以参考[Lombok feature]overview(https://projectlombok.org/features/)

**注意**：使用Lombok时，当有特殊需求时也可定制自己的代码。

### Lombok常用注解

![图片1](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828074.png)

## dev-tools

dev-tools只要类路径上的⽂件发⽣更改，使用的应用程序就会自动重新启动。

在 IDE中工作时，这可能是⼀个有用的功能，因为它为代码更改提供了非常快速的反馈循环。默认情况下，将监视类路径上指向目录的任何条目的更改。

**注意**：某些资源(例如静态资产和视图模板)不需要重新启动应用程序。

 **引入依赖**： 

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-devtools</artifactId>
	<optional>true</optional>
</dependency>
```

类路径文件发⽣更改，ctrl+f9重新构件，dev-tools自动重启项目

## Spring Initailizr

使⽤Spring Initailizr可以大量简化SpringBoot项目的开发

### 选择开发场景

- 官方脚手架：https://start.spring.io/
- 阿里脚手架：https://start.aliyun.com/

在网站中可构建项目来进行开发，也可在IDEA中进行开发。

![image-20230222181900330](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828929.png)

选择版本及所需依赖：

![image-20230222181815616](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828593.png)

### 自动引入依赖

![image-20230222182319403](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828658.png)

### 自动创建项目结构

**项目结构**：

![image-20230222182419733](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202302221828234.png)

**项目启动器**：

```java
@SpringBootApplication
public class SpringInitalizrApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringInitalizrApplication.class, args);
    }

}
```

