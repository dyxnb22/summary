>   SpringBoot概念

SpringBoot是快速开发的Spring框架，是Spring组件一站式解决方案，简化了繁重的配置，帮助我们以最少的工作量，更加健壮地使用现有的Spring功能。快速开发，快速整合，配置简化、内嵌服务容器

>   SpringBoot优点

1.   容易上手，提升开发效率，为Spring 开发提供一个更快、更简单的开发框架
2.   开箱即用，远离繁琐的配置
3.   提供了一系列大型项目通用的非业务性功能，例如：内嵌服务器、安全管理、运行数据监控、运行状况检查和外部化配置等
4.   SpringBoot总结就是使编码变简单、配置变简单、部署变简单、监控变简单等等

>   SpringBoot缺点

由于不用自己做的配置，报错时很难定位

>   SpringBoot核心注解

启动类上面的注解是@SpringBootApplication，主要包含以下3个注解：

-   @SpringBootConfiguration：组合@Configuration，实现配置文件的功能
-   @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，例如：java 如关闭数据源自动配置功能：@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class}) 
-   @ComponentScan：Spring组件扫描

>   SpringBoot日志框架

Spring Boot 支持Java Util Logging，Log4j2，Lockback(默认日志框架)

>   SpringBoot Starter工作原理

-   可以理解成对依赖的一种合成，starter会把一个或一套功能相关依赖都包含进来，避免了自己去依赖费事，还有各种包的冲突问题。大大的提升了开发效率。 并且相关配置会有一个默认值，如果我们自己去配置，就会覆盖默认值

-   提供一个自动化配置类，一般命名为 xxxAutoconfiguration，在这个配置类中通过条件注解来决定一个配置是否生效（条件注解就是 Spring 中原本就有的），然后它还会提供一系列的默认配置，也允许开发者根据实际情况自定义相关配置，然后通过类型安全的属性（spring.factories）注入 将这些配置属性注入进来，新注入的属性会代替掉默认属性。正因为如此，很多第三方框架，我们只需要引入依赖就可以直接使用了。当然，开发者也可以自定义 Starter
-   在SpringBoot启动时由@SpringBootApplication注解会自动去maven中读取每个starter中的 spring.factories文件，该文件里配置了所有需要被创建spring容器中的bean，并且进行自动配置把 bean注入SpringContext中(SpringContext是Spring的配置文件)

>   Spring2.x的新特性(和1.x相比)

-   配置变更
-   JDK版本升级。SpringBoot 2基于Spring5和JDK8，Spring 1.x用的是低版本
-   第三方类库升级
-   响应式Spring编程支持
-   HTTP/2支持
-   配置属性绑定
-   2.x配置中的中文可以直接读取，不用转码
-   Actuator的变化
-   CacheManager 的变化

>   SpringBoot支持的前端模版

thymeleaf，freemarker，jsp，官方不推荐jsp会有限制

>   运行SpringBoot的方式

1.   打包用命令或者放到容器中运行
2.   用 Maven/Gradle 插件运行
3.   直接执行 main 方法运行

>   SpringBoot 需要独立的容器运行吗

可以不需要，内置了 Tomcat/Jetty 等容器

>   开启Spring Boot 特性的方式

1.   继承spring-boot-starter-parent项目
2.   导入spring-boot-dependencies项目依赖

>   SpringBoot 实现热部署有哪几种方式

-   Spring Loaded
-   Spring-boot-devtools
-   Jrebel
-   模版热部署

>   SpringBoot事务的使用

首先使用注解EnableTransactionManagement开启事物之后，然后在 Service方法上添加注解Transactional

>   Async异步调用

只需要在启动类加入@EnableAsync，在方法上使用@Async注解即可实现方法的异步调用

>   如何在SpringBoot启动的时候运行一些特定的代码

可以实现接口ApplicationRunner 或者CommandLineRunner，它们都只提供了一个run方法

>   SpringBoot配置途径(按优先级)

1.   命令行参数 

2. java:comp/env里的JNDI属性
2. JVM系统属性
2. 操作系统环境变量
2. 随机生成的带random.*前缀的属性（在设置其他属性时，可以引用它们，比如$｛random. long｝）
2. 应用程序以外的application.properties或者appliaction.yml文件 
2. 打包在应用程序内的application.properties或者appliaction.yml文件
2. 通过@PropertySource标注的属性源
2. 默认属性

>   SpringBoot读取配置的方式

可以通过 @PropertySource，@value，@Environment， @ConfigurationPropertie注解来绑定变量

>   application.properties和application.yml文件可放位置？优先级？

1.   外置，在相对于应用程序运行目录的/config子目录里
2.   外置，在应用程序运行的目录里
3.   内置，在config包内
4.   内置，在Classpath根目录

>   JavaConfig

Spring3.0引入了它，它提供了配置 Spring IOC 容器的纯Java方法，有助于避免使用 XML配置。使用JavaConfig 的优点在于：

-   面向对象的配置。由于配置被定义为JavaConfig 中的类，因此用户可以充分利用Java 中的面向对象功能。一个配置类可以继承另一个，重写它的@Bean方法等
-   减少或消除 XML 配置。基于依赖注入原则的外化配置的好处已被证明。但是，许多开发人员不希望在XML 和Java之间来回切换。JavaConfig 为开发人员提供了一种纯Java方法来配置与XML配置概念相似的Spring容器。从技术角度来讲，只使用JavaConfig 配置类来配置容器是可行的，但实际上很多人认为将JavaConfig 与 XML混合匹配是理想的
-   类型安全和重构友好。JavaConfig 提供了一种类型安全的方法来配置 Spring容器。由于 Java 5.0对泛型的支持，现在可以按类型而不是按名称检索bean，不需要任何强制转换或基于字符串的查找

常用的JavaConfig

-   @Configuration：在类上打上写下此注解，表示这个类是配置类
-   @ComponentScan：在配置类上添加@ComponentScan注解。该注解默认会扫描该类所在的包下所有的配置类
-   @Bean：bean的注入
-   @EnableWebMvc： 相当于xml的< mvc:annotation-driven > 
-   @ImportResource： 相当于xml的< import resource="applicationContext- cache.xml" >

>   SpringBoot自动配置原理

主要是SpringBoot的启动类上的核心注解SpringBootApplication注解主配置类，有了这个主配置类启动时就会为SpringBoot开启一个@EnableAutoConfiguration注解自动配置功能
该注解引入了AutoConfigurationlmportSelector

有了这个EnableAutoConfiguration的话就会： 

1.   从配置文件META_INF/Spring.factories加载可能用到的自动配置类
2.   去重，并将exclude和excludeName属性携带的类排除
3.   过滤，将满足条件(@Conditional)的自动配置类返回

>   SpringBoot配置加载顺序

1.   properties文件
2.   YAML文件(不支持@PropertySource注解导入自定义的YAML配置)
3.   系统环境变量
4.   命令行参数

>   Spring Boot 是否可以使用 XML配置

Spring Boot 推荐使用Java 配置，但也可以使用 XML 配置，通过 @lmportResource 注解引入一个XML配置

>   SpringBoot核心配置文件

单纯做 Spring Boot 开发，可能不太容易遇到bootstrap.properties配置文件，但是在结合SpringCloud 时，这个配置就会经常遇到了，特别是在需要加载一些远程配置文件的时侯。bootstrap.yml优先于application.yml

spring boot 核心的两个配置文件：

-   bootstrap(yml 或者properties)：boostrap由父 ApplicationContext 加载的，比applicaton优先加载，配置在应用程序上下文的引导阶段生效。一般来说我们在 SpringCloud 配置就会使用这个文件。且 boostrap 里面的属性不能被覆盖
-   application(.yml 或者.properties)： 由ApplicatonContext 加载，用于 spring boot 项目的自动化配置

>   Spring Profiles

在项目的开发中，有些配置文件在开发、测试或者生产等不同环境中可能是不同的。Spring Profiles 允许用户根据配置文件(dev, test,prod等)来注册bean。例如 application-dev.properties 

>   如何激活某个环境的配置

spring.profiles.active=dev

>   SpringBoot多数据源拆分

先在properties配置文件中配置两个数据源，创建分包mapper，使用@ConfigurationProperties读取properties中的配置，使用@MapperScan注册到对应的mapper包中

>   SpringBoot多数据源事务管理

-   第一种方式是在service层的@TransactionManager中使用transactionManager指定DataSourceConfig中配置的事务
-   第二种是使用jta-atomikos实现分布式事务管理

>   保护SpringBoot应用的方法

-   在生产中使用HTTPS
-   使用Snyk检查你的依赖关系
-   升级到最新版本
-   启用CSRF保护
-   使用内容安全策略防止XSS攻击

>   CSRF

CSRF代表跨站请求伪造。这是一种攻击，迫使最终用户在当前通过身份验证的web 应用 程序上执行不需要的操作。CSRF 攻击专门针对状态改变请求，而不是数据窃取，因攻击者无法查看对伪造请求的响应

>   如何实现SpringBoot的安全性

使用 spring-boot-starter-security依赖项，并且必须添加安全配置。它只需要很少的代码。配置类将必须扩展WebSecurityConfigurerAdapter 并覆盖其方法

>   比较一下 Spring Security 和 Shiro 的优缺点

由于 Spring Boot 官方提供了大量的非常方便的开箱即用的Starter，包括 Spring Security 的 Starter ，使得在 Spring Boot 中使用Spring Security 变得更加容易，甚至只需要添加一个依赖就可以保护所有的接口。Shiro 和 Spring Security 相比，主要有如下一些特点：

-   Spring Security 是一个重量级的安全管理框架，Shiro 则是一个轻量级的安全管理框架
-   Spring Security 概念复杂，配置繁琐；Shiro概念简单、配置简单
-   Spring Security 功能强大；Shiro功能简单

>   SpringBoot中的跨域问题

跨域可以在前端通过JSONP来解决，但是JSONP只可以发送 GET 请求，无法发送其他类型的请求，在 RESTful 风格的应用中，就显得非常鸡肋，因此我们推荐在后端通过CORS(Cross-origin resource sharing)来解决跨域问题。这种解决方案并非 Spring Boot 特有的，在传统的SSM框架中，就可以通过CORS 来解决跨域问题，只不过之前我们是在XML文件中配置CORS， 现在可以通过实现WebMvcConfigurer接口然后重写addCorsMappings方法解决跨域问题

>   SpringBoot监视器

SpringBoot actuator 是spring启动框架中的重要功能之一。Spring boot 监视器可帮助您访问生产环境中正在运行的应用程序的当前状态。有几个指标必须在生产环境中进行检查和监控。即使一 外部应用程序可能正在使用这些服务来向相关人员触发警报消息。监视器模块公开了一组可直接作为 HTTP URL 访问的REST 端点来检查状态

配置监控只需要引入spring-boot-starter-actuator依赖

>   如何在SpringBoot中禁用 Actuator 端点安全性

默认情况下，所有敏感的HTTP 端点都是安全的，只有具有ACTUATOR 角色的用户才能访问它们。安全性是使用标准的HttpServletRequest.isUserInRole 方法实施的。我们可以使用 management.security.enabled = false 来禁用安全性。只有在执行机构端点在防火墙后访问时，才建议禁用安全性。

>   SpringBoot全局异常处理

@ControllerAdvice  @ExceptionHandler。通过实现ControllerAdvice类，来处理控制器类抛出的所有异常

>   如何监视SpringBoot所有微服务

Spring Boot 提供监视器端点以监控各个微服务的度量。这些端点对于获取有关应用程序的信息（如它们是否已启动）以及它们的组件（如数据库等）是否正常运行很有帮助。但是，使用监视器的一个主要缺点或困难是，我们必须单独打开应用程序的知识点以了解其状态或健康状况。想象一下涉及50个应用程序的微服务，管理员将不得不击中所有50个应用程序的执行终端。为了帮助我们处理这种情况，我们将使用位于的开源项目。它建立在 Spring Boot Actuator 之上，它提供 了一个 Web Ul，使我们能够可视化多个应用程序的度量

>   SpringBoot性能优化

-   如果项目比较大，类比较多，不使用@SpringBootApplication，采用@Compoment指定扫包范围

-   在项目启动时设置jVM初始内存和最大内存相同
-   将springboot内置服务器由tomcat设置为undertow

>   SpringBoot微服务如何实现session共享

常见的方案就是 Spring Session + Redis 来实现 session共享。将所有微服务的 session 统一保存在 Redis 上，当各个微服务对 session 有相关的读写操作时，都去操作 Redis 上的 session。这样就实现了 session 共享，Spring Session 基于 Spring 中的代理过滤器实现，使得session的同步操作对开发人员而言是透明的，非常简便

>   SpringBoot定时任务

在 Spring Boot 中使用定时任务主要有两种不同的方式，一个就是使用 Spring 中的 @Scheduled注解，另一个则是使用第三方框架 Quartz

>spring-boot-starter-parent 有什么用

1.   定义了Java 编译版本为1.8

2.   使用 UTF-8 格式编码

3.   继承自 spring-boot-dependencies，这个里边定义了依赖的版本，也正是因为继承了这个依赖，所以我们在写依赖时才不需要写版本号

4.   执行打包操作的配置

5.   自动化的资源过滤

6.   自动化的插件配置

7.   针对 application.properties 和 application.yml 的资源过滤，包括通过 profile 定义的不同环境的配置文件，例如 application-dev.properties 和 application-dev.yml

     总结就是打包用的

>   SpringBoot如何打包

mvn clean package

>   SpringBoot生成的jar包 和 普通jar包的区别

-   Spring Boot 项目最终打包成的jar是可执行jar，这种jar可以直接通过 java -jar xxx.jar 命 令来运行，这种jar 不可以作为普通的jar 被其他项目依赖，即使依赖了也无法使用其中的类

-   Spring Boot的jar 无法被其他项目依赖，主要还是他和普通jar 的结构不同。普通的jar 包，解压后直接就是包名，包里就是我们的代码，而 Spring Boot 打包成的可执行jar 解压后，在\BOOT- INF\classes 目录下才是我们的代码，因此无法被直接引用。如果非要引用，可以在pom.xml 文件中增加配置，将 SpringBoot 项目打包成两个jar，一个可执行，一个可引用

>   如何集成SpringBoot和ActiveMQ

使用 spring-boot-starter-activemq 依赖关系。它只需要很少的配置，并且不需要样板代码

>   如何使用SpringBoot实现分页和排序

使用Spring Data-JPA可以实现将可分页的org.springframework.data.domain.Pageable传递给存储库方法

>   什么是 Swagger？你用 Spring Boot 实现了它吗

Swagger 广泛用于可视化 API，使用Swagger UI 为前端开发人员提供在线沙箱。Swagger 是 用于生成 RESTful web 服务的可视化表示的工具，规范和完整框架实现。它使文档能够以与服务器相同的速度更新。当通过Swagger 正确定义时，消费者可以使用最少量的实现逻辑来理解远程服务并与其进行交互。因此，Swagger 消除了调用服务时的猜测

>   Spring Batch

SpringBoot Batch 提供可重用的函数，这些函数在处理大量记录时非常重要，包括日志/跟踪，事务管理，作业处理统计信息，作业重新启动，跳过和资源管理。它还提供了更先进的技术服务和功能，通过优化和分区技术，可以实现极高批量和高性能批处理作业。简单以及复杂的大批量批处理作业可以高度可扩展的方式利用框架处理重要大量的信息

>   FreeMaker模版

FreeMarker 是一个基于Java 的模板引擎，最初专注于使用MVC软件架构进行动态网页生 成。使用 Freemarker 的主要优点是表示层和业务层的完全分离。程序员可以处理应用程序代码，而设计人员可以处理 html 页面设计。最后使用 freemarker 可以将这些结合起来，给出最终的输出页面

>   WebSocket

WebSocket 是一种计算机通信协议，通过单个TCP 连接提供全双工通信信道

Websocket 是双向的 -使用 WebSocket 客户端或服务器可以发起消息发送

WebSocket 是全双工的 -客户端和服务器通信是相互独立的

单个TCP连接 -初始连接使用 HTTP，然后将此连接升级到基于套接字的连接。然后这个单一连接用于所有未来的通信 

Light-与 http 相比，WebSocket 消息数据交换要轻得多

>   SpringBoot如何兼容Spring项目

在启动类加： @ImportResource(locations = {"classpath:spring.xml"})

>   获得Bean装配报告信息访问哪个端点

/beans 端点

>   关闭应用程序访问哪个端点

/shutdown 该端点默认是关闭的，如果开启，需要配置 endpoints.shutdown.enabled=true

>   查看发布应用信息访问哪个端点

/info

>   SpringBoot集成Mybatis

mybatis-spring-boot-starter

>   编写测试用例的注解

@SpringBootTest