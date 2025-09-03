# Spring概述

>   Spring概念

Spring是一个Java企业级应用的开源开发框架，为Java应用程序的开发提供了综合、广泛的基础性支持的Java平台，使得开发人员可以专注于应用程序的开发，在开发环境中安心的集成Spring框架，不必担心Spring是如何在后台进行工作的。

>   Spring框架的好处

-   DI使得使得构造器和JavaBean properties文件中的依赖关系一目了然
-   轻量
-   Spring利用了已有的技术比如ORM框架、logging框架、J2EE、Quartz和JDK Timer，以及其他视图技术
-   Spring框架是按照模块的形式来组织的。由包和类的编号就可以看出其所属的模块，开发者仅仅需要选用他们需要的模块即可
-   要测试一项用Spring开发的应用程序十分简单，因为测试相关的环境代码都已经囊括在框架中了。更加简单的是，利用JavaBean形式的POJO类，可以很方便的利用依赖注入来写入测试数据
-   Spring的Web框架亦是一个精心设计的Web MVC框架，为开发者提供一个新的选择
-   Spring提供了一个便捷的事务管理接口，适用于小型的本地事物处理(比如在单DB的环境下)和复杂的共同事物处理(比如利用JTA的复杂DB环境)

>   IOC (控制反转)

在使用控制反转的情况下，业务逻辑的流程是由对象关系图来决定的，该对象关系图由装配器负责实例化，这种实现方式还可以将对象之间的关联关系的定义抽象化。而绑定的过程是通过依赖注入实现的。

Spring中的 org.springframework.beans 包和 org.springframework.context包构成了Spring框架IoC容器的基础。

BeanFactory 接口提供了一个先进的配置机制，使得任何类型的对象的配置成为可能。ApplicationContext接口对BeanFactory(是一个子接口)进行了扩展，在BeanFactory的基础上添加了其他功能，比如与Spring的AOP更容易集成，也提供了处理message resource的机制(用于国际化)、事件传播以及应用层的特别配置，比如针对Web应用的WebApplicationContext。

org.springframework.beans.factory.BeanFactory是Spring IoC容器的具体实现，用来包装和管理前面提到的各种bean。BeanFactory接口是Spring IoC 容器的核心接口。



# Spring Beans

>   BeanFactory和ApplicationContext的区别

BeanFactory 可以理解为含有bean集合的工厂类。BeanFactory 包含了各种bean的定义，以便在接收到客户端请求时将对应的bean实例化。

BeanFactory还能在实例化对象的时生成协作类之间的关系。此举将bean自身与bean客户端的配置中解放出来。BeanFactory还包含了bean生命周期的控制，调用客户端的初始化方法(initialization methods)和销毁方法(destruction methods)。

从表面上看，application context如同bean factory一样具有bean定义、bean关联关系的设置，根据请求分发bean的功能。但application context在此基础上还提供了其他的功能。

以下是三种较常见的 ApplicationContext 实现方式

在FileSystemResource 中需要给出spring-config.xml文件在你项目中的相对路径或者绝对路径。在ClassPathResource中spring会在ClassPath中自动搜寻配置文件

~~~java
// 从classpath的xml配置文件中读取上下文
ApplicationContext context = new ClassPathXmlApplicationContext(“bean.xml”);
// 从文件系统的xml配置文件中读取上下文
ApplicationContext context = new FileSystemXmlApplicationContext(“bean.xml”);
// 由Web应用的XML文件读取上下文
ServletContext servletContext = request.getSession().getServletContext();
ApplicationContext ctx = WebApplicationContextUtils.getWebApplicationContext(servletContext);
~~~

>   DI (依赖注入)

依赖注入是在编译阶段尚未知所需的功能是来自哪个的类的情况下，将其他对象所依赖的功能对象实例化的模式。这就需要一种机制用来激活相应的组件以提供特定的功能。依赖注入是控制反转的基础。

依赖注入三种实现方式：

1.   构造器注入
2.   Setter方法注入
3.   接口注入

>   Spring配置方式

1.   基于XML配置
2.   基于注解的配置
3.   基于Java的配置

>   基于Java的配置

通过@Configuration 和 @Bean

~~~java
@Configuration
public class AppConfig
{
    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
// xml等效于
<beans>
    <bean id="myService" class="com.howtodoinjava.services.MyServiceImpl"/>
</beans>
// 实例化
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
    MyService myService = ctx.getBean(MyService.class);
    myService.doStuff();
} 
// 如果使用组件扫描，在AppConfig上加上
@ComponentScan(basePackages = "com.howtodoinjava")
~~~



>   注解配置Spring

xml优先级更高

1.   @Required：该注解应用于设值方法，验证某个bean的特定属性是否被正确的设置
2.   @Autowired：该注解应用于有值设值方法、非设值方法、构造方法和变量
3.   @Qualifier：该注解和@Autowired注解搭配使用，用于消除特定bean自动装配的歧义，用来取消Spring不能取消的bean应用

4.   JSR-250 Annotations：Spring支持基于JSR-250注解的以下注解，@Resource、@PostConstruct 和 @PreDestroy

>   Spring Bean的生命周期

Springbeanfactory 负责管理在Spring容器中被创建的bean的生命周期。Bean的生命周期由两组回调(call back)方法组成

1.   初始化之后调用的回调方法
2.   销毁之前调用的回调方法

Spring框架提供了以下四种方式来管理bean的生命周期事件：

-   InitializingBean和DisposableBean回调接口

-   针对特殊行为的其他Aware接口

-   Bean配置文件中的Custom init()方法和destroy()方法

-   @PostConstruct和@PreDestroy注解方式

>   Spring Bean的范围

1.   singleton：这种bean范围是默认的，这种范围确保不管接受到多少个请求，每个容器中只有一个bean的实例，单例的模式由beanfactory自身来维护
2.   prototype：原形范围与单例范围相反，为每一个bean请求提供一个实例
3.   request：在请求bean范围内会每一个来自客户端的网络请求创建一个实例，在请求完成以后，bean会失效并被垃圾回收器回收
4.   session：与请求范围类似，确保每个session中有一个bean的实例，在session过期后，bean会随之失效。
5.   global-session：global-session和Portlet应用相关。当你的应用部署在Portlet容器中工作时，它包含很多portlet。如果你想要声明让所有的portlet共用全局的存储变量的话，那么这全局变量需要存储在global-session中

全局作用域与Servlet中的session作用域效果相同。

>   Spring的嵌入beans

在Spring框架中，无论何时bean被使用时，当仅被调用了一个属性。一个明智的做法是将这个bean声明为内部bean。内部bean可以用setter注入“属性”和构造方法注入“构造参数”的方式来实现

>   Spring中单例Bean是否线程安全

Spring框架并没有对单例bean进行任何多线程的封装处理。但实际上，大部分的Spring bean并没有可变的状态，如果你的bean有多种状态的话(比如 View Model 对象)，就需要自行保证线程安全。最浅显的解决办法就是将多态bean的作用域由singleton变更为prototype

>   如何在Spring中注入集合

<list>  <set>  <map>  <props> (支持注入键和值都是字符串类型的键值对)

>   Spring中的自动装配

~~~xml
<bean id="employeeDAO" class="com.howtodoinjava.EmployeeDAOImpl" autowire="byName" />
~~~

或者使用@Autowired

开启方式

~~~xml
<beans>
    <context:annotation-config />
</beans>
或者
<beans>
<bean class="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>
</beans>
~~~



>   自动装配模式

1.   no：这是Spring框架的默认设置，在该设置下自动装配是关闭的，开发者需要自行在bean定义中用标签明确的设置依赖关系
2.   byName：该选项可以根据bean名称设置依赖关系。容器将根据bean的名称自动在在配置文件中查询匹配的bean
3.   byType：该选项可以根据bean类型设置依赖关系。容器将根据bean的类型自动在在配置文件中查询匹配的bean
4.   constructor：造器的自动装配和byType模式类似，但是仅仅适用于与有构造器相同参数的bean，如果在容器中没有找到与构造器参数类型一致的bean，那么将会抛出异常
5.   autodetect：该模式自动探测使用构造器自动装配或者byType自动装配。首先，首先会尝试找合适的带参数的构造器，如果找到的话就是用构造器自动装配，如果在bean内部没有找到相应的构造器或者是无参构造器，容器就会自动选择byTpe的自动装配方式



>   构造方法注入和设值注入的区别

1.   在设值注入方法支持大部分的依赖注入，如果我们仅需要注入int、string和long型的变量，我们不要用设值的方法注入。对于基本类型，如果我们没有注入的话，可以为基本类型设置默认值。在构造方法注入不支持大部分的依赖注入，因为在调用构造方法中必须传入正确的构造参数，否则的话为报错
2.   设值注入不会重写构造方法的值。如果我们对同一个变量同时使用了构造方法注入又使用了设置方法注入的话，那么构造方法将不能覆盖由设值方法注入的值。很明显，因为构造方法尽在对象被创建时调用
3.   在使用设值注入时有可能还不能保证某种依赖是否已经被注入，也就是说这时对象的依赖关系有可能是不完整的。而在另一种情况下，构造器注入则不允许生成依赖关系不完整的对象
4.   在设值注入时如果对象A和对象B互相依赖，在创建对象A时Spring会抛出sObjectCurrentlyInCreationException异常，因为在B对象被创建之前A对象是不能被创建的，反之亦然。所以Spring用设值注入的方法解决了循环依赖的问题，因对象的设值方法是在对象被创建之前被调用的

>   Spring中不同类型的事件

Spring的ApplicationContext 提供了支持事件和代码中监听器的功能。

我们可以创建bean用来监听在ApplicationContext 中发布的事件。ApplicationEvent类和在ApplicationContext接口中处理的事件，如果一个bean实现了ApplicationListener接口，当一个ApplicationEvent 被发布以后，bean会自动被通知

5种标准事件：

1.   上下文更新事件(ContextRefreshedEvent)：该事件会在ApplicationContext被初始化或者更新时发布。也可以在调用ConfigurableApplicationContext 接口中的refresh()方法时被触发
2.   上下文开始事件(ContextStartedEvent)：当容器调用ConfigurableApplicationContext的Start()方法开始/重新开始容器时触发该事件
3.   上下文停止事件(ContextStoppedEvent)：当容器调用ConfigurableApplicationContext的Stop()方法停止容器时触发该事件
4.   上下文关闭事件(ContextClosedEvent)：当ApplicationContext被关闭时触发该事件。容器被关闭时，其管理的所有单例Bean都被销毁
5.   请求处理事件(RequestHandledEvent)：在Web应用中，当一个http请求(request)结束触发该事件

# Spring注解



# Spring数据访问



# Spring AOP