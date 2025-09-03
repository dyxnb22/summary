>   MyBatis

MyBatis 是一个可以自定义SQL、存储过程和高级映射的持久层框架

>   讲下 MyBatis 的缓存

MyBatis 的缓存分为一级缓存和二级缓存，一级缓存放在 session 里面，默认就有，二级缓存放在它的命名空间里，默认是不打开的，使用二级缓存属性类需要实现 Serializable 序列化接口（可用来保存对象的状态），可在它的映射文件中配置<cache/> 

>   Mybatis 是如何进行分页的？分页插件的原理是什么

1.   Mybatis 使用RowBounds 对象进行分页，也可以直接编写sql实现分页，也可以使用 Mybatis 的分页插件
2.   分页插件的原理：实现 Mybatis 提供的接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写 sql

>   Mybatis 的插件运行原理，以及如何编写一个插件？

1.   Mybatis 仅可以编写针对 ParameterHandler、ResultSetHandler、StatementHandler、 Executor 这4种接口的插件，Mybatis 通过动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这4种接口对象的方法时，就会进入拦截方法，具体就是 InvocationHandler 的 invoke方法，当然，只会拦截那些你指定需要拦截的方法
2.   实现 Mybatis 的 Interceptor 接口并复写 intercept方法，然后在给插件编写注解，指定要拦截哪一个接口的哪些方法即可，记住，别忘了在配置文件中配置你编写的插件

>   Mybatis 动态sql是做什么的？简述一下动态sql 的执行原理

Mybatis 动态sql可以让我们在Xml 映射文件内，以标签的形式编写动态sql，完成逻辑判断和动态拼接sql 的功能

使用 OGNL 从sql参数对象中计算表达式的值，根据表达式的值动态拼接sql，以此来完成动态sql 的功能

>   #{}和${}的区别

#是预编译处理(可以防止注入)，$是字符串替换

>   为什么Mybatis 是半自动ORM映射工具？它与全自动的区别在哪里

Hibernate 属于全自动 ORM 映射工具，使用 Hibernate 可以根据对象关系模型直接查询，对象/关系映射能力强，数据库无关性好；而Mybatis 需要手动编写sql来完成

>   Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？

Mybatis 仅支持 association(一对一)关联对象和 collection(一对多) 关联集合对象的延迟加载。在Mybatis 配置文件中，可以配置是否启用延迟加载lazyLoadingEnabled=truelfalse

它的原理是，使用CGLIB创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用 a.getB().getName()，拦截器 invoke()方法发现 a.getB()是 null 值，那么就会单独发送事先保存好的查询关联B对象的sql，把B查询上来，然后调用 a.setB(b)，于是a的对象b属性就有值了，接着完成 a.getB().getName（）方法的调用。这就是延迟加载的基本原理

>   Mybatis 映射文件中，如果A 标签通过 include 引用了B标签的内容，B 标签能否定义在A 标签的后面

虽然Mybatis 解析 Xml 映射文件是按照顺序解析的，但是被引用的B标签依然可以定义在任何地方。

原理是Mybatis 解析A标签，发现A标签引用了B标签，但是B标签尚未解析到， 尚不存在，此时，Mybatis 会将A 标签标记为未解析状态，然后继续解析余下的标签， 包含B标签，待所有标签解析完毕，Mybatis 会重新解析那些被标记为未解析的标签，此时再解析 A 标签时，B标签已经存在，A标签也就可以正常解析完成了

>   Mybatis 的xml 映射文件和 Mybatis 内部数据结构之间的映射关系

Mybatis 将所有 Xml 配置信息都封装到 All-In-One 重量级对象 Configuration 内部。在 Xml 映射文件中，<parameterMap>标签会被解析 ParameterMap 对象，其每个子元素会被解析 ParameterMapping 对象。<resultMap>标签会被解析 ResultMap 对象，其每个子元素会被解析为 ResultMapping 对象。每一个<select>、<insert>、<update>、<delete>标签 均会被解析为 MappedStatement 对象，标签内的sql 会被解析为 BoundSql对象

>   什么是 MyBatis 的接口绑定

MyBatis 中任意定义接口，然后把接口里面的方法和SQL语句绑定。一种是通过注解绑定(sql语句简单)，另外一种就是通过xml 里面写SQL来绑定(sql语句复杂)

>   MyBatis 实现一对一有几种方式

有联合查询和嵌套查询，联合查询是几个表联合查询，只查询一次，通过在 resultMap 里面 配置 association 节点配置一对一的类就可以完成；嵌套查询是先查一个表，根据这个表里面的结果的外键id，去再另外一个表里面查询数据，也是通过 association 配置，但另外一个表的查询通过 select 属性配置

>   Mybatis 能执行一对一、一对多的关联查询吗

能，Mybatis 不仅可以执行一对一、一对多的关联查询，还可以执行多对一，多对多的关联查询，多对一查询，其实就是一对一查询，只需要把 selectOne()修改为 selectList()即可；多对多查询，其实就是一对多查询，只需要把 selectOne()修改 selectList()即可

关联对象查询，有两种实现方式，一种是单独发送一个sql去查询关联对象，赋给主对象，然后返回主对象。另一种是使用嵌套查询，嵌套查询的含义为使用join 查询，一部分列是A对象的属性值，另外一部分列是关联对象B的属性值，好处是只发一个sql 查询， 就可以把主对象和其关联对象查出来

>   一级、二级缓存 

-   一级缓存：基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为 Session，当 Session flush 或 close 之后，该 Session 中的所有Cache就将清空
-   二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache, HashMap 存 储，不同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。要开启二级缓存，你需要在你的 SQL 映射文件中添加一行：<cache/> 
-   对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存 Namespaces)的进行了 C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear

