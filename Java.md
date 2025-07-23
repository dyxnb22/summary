# 概述

>   Java语言的特点

1.   面向对象(易维护、易复用、易扩展) (面向过程：高性能，不需要实例化)

2.   平台无关性 (JVM)；
3.   健壮性(强类型机制、异常处理、垃圾自动回收)；
4.   安全性好；
5.   支持多线程（C++语言没有内置的多线程机制，因此必须调用操作系统的多线程功能来进行多线程程序设计，而 Java 语言却提供了多线程支持）；
6.   提供了对Web应用开发的支持
7.   编译与解释并存，是解释性语言；
8.   简单易学，功能强大(相较于C++，都是面向对象，但摒弃指针、多继承，有自动内存管理机制)


>   JDK 1.5后的三大版本

Java SE (标准版) 、 Java EE (企业版)、Java ME (微型版)

>   采用字节码(class文件，只面向虚拟机)的好处

Java语言通过字节码的方式（编译器 --> 解释器 --> 机器），在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以lava程序运行时比较高效，而且，由于字节码并不专对一种特定的机器，因此，Java程序无须重新编译便可在多种不同的计算机上运行。

>   Oracle JDK 和 OpenJDK的对比

-   前者3年发布一次，后者每三个月发布一次
-   前者不是完全开源，是后者的一个实现；后者完全开源，并且是一个参考模型
-   前者更加稳定
-   在响应性和JVM性能方面，前者性能更好
-   OracleJDK不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本
-   OracleJDK根据二进制代码许可协议获得许可，而OpenJDK根据GPL v2许可获得许可。

>   Java应用程序 与 小程序之间的差别？主类又有什么区别

Java应用程序从主程序main()启动( JVM 在运行的时候会首先查找 main 方法 )，**主类**是指包含main()的类，不一定要求是public类。 在Java 7之前，你可以通过使用静态初始化运行 Java 类。但是，从Java 7 开始，没有 main 方法我们不能运行Java类。

main方法一定得是static的，这样JVM在调用它的时候才无需实例化

main可以重载，但不能被覆盖，作用域不能改变

main方法可以同步，synchronized 允许用于main方法的声明中

可以在Java中终结main方法

applet小程序主要嵌在浏览器页面运行(调用init()线程或者run()来启动)，**主类**是继承自系统类JApplet或者Applet的子类，要求必须是public

>   一个".java"源文件中是否可以包括多个类（不是内部类）？有什么限制 ？

可以，只有一个类是用public修饰

**没有人说过 Java 的 Class 名字必须和其文件名相同。但 public class 的名字必须和文件名相同**

>   JDK中常用的包

-   java.lang: 这个是系统的基础类
-   java.io: 这里面是所有输入输出有关的类，比如文件操作等
-   java.nio: 为了完善io包中的功能，提高 io 包中性能而写的一个新包
-   java.net: 这里面是与网络有关的类
-   java.util: 这个是系统辅助类，特别是集合类
-   java.sql: 这个是数据库操作的类

>   import java 和 import javax

最开始javax作为拓展，后面逐渐拓展成Java API的组成部分，没有区别了

>   Integer 和 int 比较

会自动拆箱成int。如果整型字面量的值在-128到127之间，那么自动装箱时不会new新的Integer对象，而是直接引用常量池中的 Integer对象，超过范围 a1==b1的结果是false

~~~java
Integer a = new Integer(3); // java9以后被移除了，应该使用Integer.valueof() 或者 自动装箱
Integer b = 3; // a != b
Integer a1 = 127;
Integer b1 = 127; // a == b
Integer a1 = 128;
Integer b1 = 128; // a != b
~~~

>   字节序定义 以及 Java属于哪种字节序

字节序是指多字节数据在计算机内存中存储或网络传输时个字节的存储顺序

1.   小端：低位字节存放在内存的低地址端，高位字节存放在内存的高地址端

2.   大端：高位字节存放在内存的低地址端，低位字节存放在内存的高地址端

Java语言的字节序是大端

>   构造方法、成员变量初始化以及静态成员变量三者的初始化顺序

先后顺序：静态成员变量、成员变量、构造方法。 

详细的先后顺序：父类静态变量、父类静态代码块、子类静态变量、子类静态代码块、父类非静态变量、父类非静态代码块、父类构造函数、子类非静态变量、子类非静态代码块、子类构造函数。

>   Class对象

Java中对象可以分为实例对象和Class对象，每一个类都有一个Class对象，其包含了与该类有关的信息。 

获取Class对象的方法： 

-   Class.forName("类的全限定名”) 
-   实例对象.getClass()
-   类名.class

>   注解

Java 注解用于为 Java 代码提供元数据。作为元数据，注解不直接影响你的代码执行，但也有一些类型的注解实际上可以用于这一目的。

其可以用于提供信息给编译器，在编译阶段时给软件提供信息进行相关的处理，在运行时处理写相应代码，做对应操作。

>   元注解

元注解可以理解为注解的注解，即在注解中使用，实现想要的功能。其具体分为： 

-   @Retention：表示注解存在阶段是保留在源码，还是在字节码(类加载)或者运行期(JVM中运行)
-   @Target：表示注解作用的范围
-   @Documented：将注解中的元素包含到 Javadoc 中去
-   @Inherited：一个被@Inherited注解了的注解修饰了一个父类，如果他的子类没有被其他注解修饰，则它的子类也继承了父类的注解
-   @Repeatable：被这个元注解修饰的注解可以同时作用一个对象多次，但是每次作用注解又可以代表不同的含义

>   Object类常用方法

-   hashCode：通过对象计算出的散列码。用于map型或equals方法。 需要保证同一个对象多次调用该方法，总返回相同的整型值
-   equals： 判断两个对象是否一致。需保证equals方法相同对应的对象hashCode也相同
-   toString：用字符串表示该对象  
-   clone：深拷贝一个对象

>   Java中线程安全的基本数据结构

-   HashTable：哈希表的线程安全版，效率低 

-   ConcurrentHashMap：哈希表的线程安全版，效率高，用于替代HashTable 
-   Vector：线程安全版Arraylist 
-   Stack：线程安全版栈 
-   BlockingQueue及其子类：线程安全版队列

# 基础语法

## 数据类型

-   基本数据类型

<img src="pics/image-20250720114124399.png" alt="image-20250720114124399" style="zoom:50%;" align="left"/>

-   引用数据类型：class interface 数组

>   switch数据类型

在Java 5以前，switch(expr)中，expr 只能是 byte、short、char、int。从Java5 开始，Java中 引入了枚举类型，expr 也可以是 enum 类型，从Java 7 开始，expr 还可以是字符串(String)， 但是**长整型(long)**在目前所有的版本中都是不可以的。

>   最有效率的2 乘 8

2 << 3

>   floatf=3.4；是否正确

 不正确。3.4 是双精度数，将双精度型(double)赋值给浮点型(float)属于下转型(down- casting，也称为窄化)会造成精度损失，因此需要强制类型转换float f=(float)3.4；或者写成 float f=3.4F

>   short s1=1;s1 =s1+1；有错吗？short s1 =1;s1+=1；有错吗

对于 short s1 = 1;s1=s1 +1：由于1是int类型，因此s1+1 运算结果也是int型，需要强制转换 类型才能赋值给short型。 

而 short s1 = 1;s1 += 1；可以正确编译，因为 s1+=1；相当于 s1 = short(s1 + 1)；其中有隐含的强制类型转换。

>   Java语言采取什么编码?有什么特点？

Java语言采用Unicode编码标准，Unicode(标准码)，它为每个字符制订了一个唯一的数值，因此在任何的语言，平台，程序都可以放心的使用。

## 访问修饰符

private、protected不能修饰外部类，使用对象: 变量、方法

<img src="pics/image-20250720124909401.png" alt="image-20250720124909401" style="zoom:50%;" align="left"/>



## 关键字

>   goto

goto是Java的保留字，没有使用

>   break跳出多重循环

可以在外面的循环语句前定义一个标号，然后在里层循环体的代码中使用带有标号的break 语句

>   final

-   被final修饰的类不可以被**继承** 

-   被final修饰的方法不可以被**重写** 

-   被final修饰的变量不可以被**改变**，被final修饰**不可变的是变量的引用，而不是引用指向的内容**


>   出现在Java程序中的finally代码块是否一定会执行？

当遇到下面情况不会执行。

1. 当程序在进入try语句块**之前就出现异常时**会直接结束。
2. 当程序在try块中**强制退出时，如使用System.exit(0)**，也不会执行finally块中的代码。

当try/catch语句块中有return时，finally语句块中的代码**会在return之前执行**。如果try/catch/finally块中都有return语句，finally块中的return语句**会覆盖try/catch模块中的return语句**。

>   finalize

finalize是一个方法，属于Object类的一个方法，而Object类是所有类的父类，该方法一般由垃圾回收器来调用，当我们调用System.gc()方法的时候，由垃圾回收器调用finalize()，回收垃圾，一个对象是否可回收的最后判断。

>   this, super

this可以引用本类中另一种形式的构造函数;super可以调用父类中的某一个构造函数

都需要为构造函数中的第一条，不能同时出现在同一个构造函数中，均不可以在static环境中使用

本质上，this是一个指向本对象的指针，super是一个java关键字

~~~java
public Person(String A, String B){
  this(A);
  this.B = B;
}
~~~

>   staitic

-   static的主要意义是在于创建独立于具体对象的域变量或者方法, 这些变量和方法被类的实例对象所共享

-   static关键字还有一个比较关键的作用就是 用来**形成静态代码块以优化程序性能**。static块可以置于类中的任何地方，类中可以有多个static块。在类初次被加载的时候，会按照static块的顺序来执行每个static块，并且只会执行一次 (初始化是在第一次使用的时候)

-   注意事项：1、静态只能访问静态。 2、非静态既可以访问非静态的，也可以访问静态的。

-   应用场景：1、修饰成员变量  2、修饰成员方法  3、静态代码块  4、修饰类【只能修饰内部类也就是静态内部 类】5、静态导包



## 泛型

>   概念

泛型，即“参数化类型”，解决不确定对象具体类型的问题。在编译阶段有效。在泛型使用过程中，操作的数据类型被指定为一个参数，这种参数类型在类中称为泛型类、接口中称为泛型接口和方法中称为泛型方法

>   泛型擦除

Java编译器生成的字节码是不包涵泛型信息的，泛型类型信息将在编译处理是被擦除，这个过程被称为泛型擦除

# 异常

>   分类

Java昇常分为Error(程序无法处理的错误)，和Exception(程序本身可以处理的异常)。这两个类均继承Throwable。

Error常见的有StackOverFlowError,OutOfMemoryError等等。 

Exception可分为运行时异常和非运行时异常。对于运行时异常，可以利用try catch的方式进行处理，也可以不处理。对于非运行时异常，必须处理，不处理的话程序无法通过编译。

>   简述throw与throws的区别

throw一般是用在方法体的内部，由开发者定义当程序语句出现问题后主动抛出一个异常

 throws一般用于方法声明上，代表该方法可能会抛出的异常列表。

# 反射

>   反射机制的概念

 JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。 

静态编译：在编译时确定类型，绑定对象。动态编译：运行时确定类型，绑定对象

>   反射机制的优缺点 

-   优点：运行期类型的判断，动态加载类，提高代码灵活度。 

-   缺点：性能瓶颈：反射相当于一系列解释操作，通知JVM要做的事情，性能比直接的java代码要慢很多。

>   反射机制的应用场景

框架设计(模块化开发; 动态代理设计模式; Spring/Hibernate等框架)

例子 JDBC Class.forName()加载数据库驱动程序;Spring 通过xml装载bean

>   获取反射的三种方式

1.通过new对象实现反射机制 2.通过路径实现反射机制 3.通过类名实现反射机制

<img src="pics/image-20250722115115465.png" alt="image-20250722115115465" style="zoom:50%;" align = "left"/>

-   Class类：可获得类属性方法 
-   Field类：获得类的成员变量 
-   Method类：获取类的方法信息 
-   Construct类：获取类的构造方法等信息

# 面向对象

>   三大特性

-   多态
-   封装：把一个对象的属性私有化
-   继承：子类拥有父类非private的属性和方法。

抽象：包括数据抽象和行为抽象

>   多态

父类或接口定义的引用变量可以指向子类或具体实现类的实例对象。提高了程序的拓展性。两种形式可以实现多态：继承(多个子类对同一方法的重写)和接口(实现接口并覆盖 接口中同一方法)。程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定。

多态分为编译时多态(静态的，主要是指方法的**重载**，根据参数列表的不同来区分不同的函数，在运行时谈不上多态) 和 运行时多态(动态的，通过多态绑定实现)

多态实现的三个必要条件:

-   继承
-   重写：对父类某些方法进行重新定义
-   向上转型：将子类的引用赋给父类

两种多态的机制：**重载**和**重写(覆盖)**

原则：当超类对象引用变量引用子类对象时，**被引用对象的类**型而不是引用变量的类型决定了调用谁的成员方法，但是这个**被调用的方法必须是在超类(子类)中定义过**。

好处：可替换性、可拓展性、接口性、灵活性、简化性

>   面向对象五大基本原则

-   单一职责原则
-   开放封闭原则：对拓展是开放的，对修改是封闭的
-   里氏替换原则：子类能替换父类出现在其能出现的任何地方
-   依赖倒置原则：具体实现依赖于抽象
-   接口分离原则：将不同功能拆分成不同接口



## 类与接口

>   抽象类和接口

-   抽象类是用来捕捉子类的通用特性的。接口是抽象方法的集合。 

-   从设计层面来说，抽象类是对类的抽象，是一种模板设计，接口是行为的抽象，是一种行为的规范

相同点：

-   接口和抽象类都不能实例化 
-   都位于继承的顶端，用于被其他实现或继承 
-   都包含抽象方法，其子类都必须覆写这些抽象方法

不同点：

<img src="pics/image-20250721202954275.png" alt="image-20250721202954275" style="zoom:50%;" align = "left"/>

**接口只能有方法定义，不能有方法的实现**，而抽象类可以有方法的定义与实现，但是抽象方法不能有方法体，private 和 abstract 不能同时出现。

**任何在 interface 里声明的 interface variable ，默认为 public static final**

Java8中接口中引入默认方法和静态方法，以此来减少抽象类和接口之间的差异。

当子类和父类有逻辑上的层次结构，推荐抽象类

行为模型优先选择接口

对象引用指向对象实例

抽象类不能用final修饰

>   为什么Java不支持多继承

1.   为了程序的结构能够更加清晰从而便于维护。假设Java语言支持多重继承，类C继承自类A和类B， 如果类A和B都有自定义的成员方法f()，那么当代码中调用类C的f()会产生二义性

2.   多重继承会使类型转换、构造方法的调用顺序变得复杂，会影响到性能。

>   普通类和抽象类

-   普通类不能包含抽象方法，抽象类可以包含抽象方法。 
-   抽象类不能直接实例化，普通类可以直接实例化。

## 变量与方法

成员变量有默认初始值；局部变量没有默认初始值，使用前必须赋值

>   在Java中定义一个不做事且没有参数的构造方法的作用

Java程序在执行子类的构造方法之前，如果没有用super()来调用父类特定的构造方法，则会**调用 父类中“没有参数的构造方法”**。因此，如果父类中只定义了有参数的构造方法，而在子类的构造方法中又没有用supe()来调用父类中特定的构造方法，则编译时将发生错误，因为Java程序在父类 中找不到没有参数的构造方法可供执行。解决办法是在父类里加上一个不做事且没有参数的构造方法。



## 内部类

>   分类

-   成员内部类

定义在成员位置上的非静态类，可以访问外部类所有的变量和成员

~~~java
public class outer {
  private int radius = 1;
  class Inner {
    ...
  }
}
Outer outer = new Outer();
Outer.Inner inner = Outer.new Inner()
~~~

-   局部内部类

定义在方法中的内部类。定义在实例方法中的局部类可以访问外部类的所有变量和方法，定义在静态方法中的局部类只能访问外部类的静态变量和方法。

-   匿名内部类

没有名字的内部类;只能使用一次

必须继承一个抽象类或者实现一个接口;

匿名内部类不能定义任何静态成员和静态方法;

当所在的方法的形参需要被匿名内部类使用时，必须声明为 final; 

(**原因:** 因为生命周期不一致，局部变量直接存储在栈中，当方法执行 结束后，非final的局部变量就被销毁。而局部内部类对局部变量的引用依然存在，如果局部内部类要调用局部变量时，就会出错。加了final，可以确保局部内部类使用的变量与外层的局部变量区分开，解决了这个问题。)

匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法。

-   静态内部类

静态内部类可以访问外部类所有的静态变量，但访问不了外部类的非静态变量

~~~java
public class Outer {
  ...
  static class staticInner {
    ...
  }
}

Outer.staticInner() Inner = new Outer.staticInner();
~~~

>   内部类优点

-   一个内部类对象可以访问创建它的外部类对象的内容，包括私有数据

-   内部类不为同一包的其他类所见，具有很好的封装性

-   内部类有效实现了"多重继承"，优化Java单继承的缺陷
-   匿名内部类可以很方便的定义回调

>   内部类应用场景

-   一些多算法场合 
-   解决一些非面向对象的语句块
-   适当使用内部类，使得代码更加灵活和富有扩展性
-   当某个类除了它的外部类，不再被其他的类使用时

## 重载(编译时多态)与重写(运行时多态)

>   构造器 Constructor是否可以被Override

不可以，但可以被重载

子类返回值小于等于父类，抛出的异常小于等于父类，访问修饰符大于等于父类(里氏代换原则); 

如果父类方法访问修饰符为private则子类中就不是重写(子类都访问不到)



## 对象相等判断

>   ==  、equals  和 hashCode

**==** 判断两个对象地址是否相同 (基础数据类型比较**值**，引用数据类型比较**内存地址**)

**equals**  当类覆盖了equals() 则比较两个对象的内容，否则比较两个对象，等价于 ==  (String里的 equals方法是比较对象中值，被重写过; Object是比较内存地址)

**hashCode**获取哈希吗(散列码)，定义在Object中；散列表存储的是key-value;两个对象相同，其hashCode也一定相同；但hashCode相同，它们不一定相等

hashCode()的默认行为是对堆上面的对象产生独特值，如果没重写hashCode()，则该class的两个对象无论如何都不会想等

**对象的相等**比的是内存中存放的内容是否相等而**引用相等**比较的是他们指向的内存地址是否相等



## 值传递

>   为什么Java中只有值传递

按值调用(call by value)表示方法接收的是调用者提供的值，而按引用调用(call by reference)表示方法接收的是调用者提供的变量地址。**一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值**。

一个方法不能修改一个基本数据类型的参数，改变一个对象参数状态需要获取其对象引用的拷贝

引用传递传递的是变量对应的地址

# String

比较字符串的值是否相同用 equals，比较字符串对象是否同一个用==

String>bytel］ 通过 String类的 getBytes 方法；bytel］>String 通过 new String（byte［］）构造器

>   特性

不变性(不代表引用不可变，而且可以通过反射来修改)、常量池优化、final(不可被子类继承)

<img src="pics/image-20250722120429628.png" alt="image-20250722120429628" style="zoom:50%;" align = "left"/>



>   字符型常量和字符串常量的区别

1.   形式上: 字符常量是单引号引起的一个字符，字符串常量是双引号引起的若干个字符 

2.   含义上: 字符常量相当于一个整形值(ASCII值)，可以参加表达式运算，字符串常量代表一个地址值(该字符串在内存中存放位置)

3.   占内存大小: 字符常量只占一个字节，字符串常量占若干个字节(至少一个字符结束标志)

>   String、StringBuffer、StringBuilder 有什么区别

String 不可变，线程安全，适合操作少量数据

StringBuffer 是线程安全的，适合多线程操作字符缓冲区下操作大量数据

StringBuilder 线程不安全，速度较快，适合单线程操作字符缓冲区下操作大量数据

>   字符串常量池

字符串常量池位于堆内存中，专门用来存储字符串常量，可以提高内存的使用率，避免开辟多块空 间存储相同的字符串，在创建字符串时JVM会首先检查字符串常量池，如果该字符串已经存在池中，则返回它的引用，如果不存在，则实例化一个字符串放到池中，并返回其引用。

>   String str = new String（"abc"）；创建了几个对象

创建了两个，“abc"本身创建在常量池，通过 new 又创建在堆中。String str = "i" 只分配到常量池

>   String str1 = "aaa"; String str2 =new String("aaa"); String str3 ="bbb"; String str4 = "aaabbb";
>
>   String str5 = "aaa" + "bbb" String str6 = str1 + "bbb"; String str7 = str2 + "ddd" + "eee";

str5创建了1个对象，因为由于`"aaa"`和`"bbb"`都是常量字符串，编译期会直接优化为`"aaabbb"`。此时会检查常量池，此时存在，所以只创建了一个对象

**str6创建了2个对象**，这种 "变量 + 常量" 的拼接，Java 无法在编译期完成优化，必须在**运行时**通过`StringBuilder`，处理过程如下：

1.  **创建`StringBuilder`对象**（第 1 个新对象）
    JVM 会自动实例化一个`StringBuilder`，用于执行拼接操作。
2.  **拼接并生成新`String`对象**（第 2 个新对象）
    -   先执行`append(str1)`（添加`"aaa"`）
    -   再执行`append("bbb")`（添加`"bbb"`）
    -   最后调用`StringBuilder.toString()`，在堆内存中生成一个新的`String`对象（内容为`"aaabbb"`）。
3.  最终`str6`引用的是堆中这个新生成的`String`对象，而非常量池中的`"aaabbb"`（即使`str4`已存在该常量）。

**str7创建了3个对象**，过程如下

1.  **编译期优化常量部分**
    首先，编译器会对连续的常量字符串进行合并：`"ddd" + "eee"`会被优化为`"dddeee"`（在常量池中新创建 1 个对象）。
2.  **运行时处理变量与优化后常量的拼接**
    剩余的`str2 + "dddeee"`包含变量`str2`，必须在运行时通过`StringBuilder`处理：
    -   第一步：创建`StringBuilder`对象（第 2 个新对象），用于拼接操作。
    -   第二步：调用`append(str2)`和`append("dddeee")`完成拼接后，执行`toString()`，在堆中生成新的`String`对象（内容为`"aaadddeee"`，第 3 个新对象）。

>   在使用HashMap时，用String做key的好处

HashMap 内部实现是通过key 的hashcode 来确定 value 的存储位置，因为字符串是不可变的， 所以当创建字符串时，它的 hashcode 被缓存下来，不需要再次计算，所以相比于其他对象更快。

>   为什么要把String设计为不变量？

1. 节省空间: 字符串常量存储在JVM的字符串池中可以被用户共享。
2. 提高效率: String会被不同线程共享，是线程安全的。在涉及多线程操作中不需要同步操作。
3. 安全: String常被用于用户名、密码、文件名等使用，由于其不可变，可避免黑客行为对其恶意修
    改。



# 集合

## 集合框架

>   集合框架的优点

1.   使用核心集合类降低开发成本，而非实现我们自己的集合类
2.   随着使用经过严格测试的集合框架类，代码质量会得到提高
3.   通过使用JDK 附带的集合类，可以降低代码维护成本
4.   复用性和可操作性

>   集合框架中的泛型的优点

1.   Java1.5 引入了泛型，所有的集合接口和实现都大量地使用它
2.   泛型允许我们为集合提供一个可以容纳的对象类型，因此，如果你添加其它类型的任何元素，它会在编译时报错
3.   这避免了在运行时出现 ClassCastException，因为你将会在编译时得到报错信息
4.   泛型也使得代码整洁，我们不需要使用显式转换和 instanceOf 操作符
5.   它也给运行时带来好处，因为不会产生类型检查的字节码指令

>   为什么Collection不从Cloneable 和 Serializable接口继承

如何维护元素由Collection的具体实现决定。在所有的实现中授权克隆和序列化，最终导致更少的灵活性和更多的限制。特定的实现应该决定它是否可以被克隆和序列化。

>   哪些集合类提供对元素的随机访问

ArrayList、HashMap、TreeMap、HashTable

>   哪些集合类是线程安全的

Vector、HashTable、Properties、Stack

>   并发集合类概念

允许在迭代时修改集合，被设计成fail-fast。包括CopyOnWriteArrayList、 ConcurrentHashMap、CopyOnWriteArraySet

>   Comparable 和 Comparator接口区别

前者提供自然排序，后者提供不同的排序算法

>   当一个集合被作为参数传递给一个函数时，如何才可以确保函数不能修改它？

在作为参数传递之前，我们可以使用 Collections.unmodifiableCollection(Collection c)方法创建一个只读集合， 这将确保改变集合的任何操作都会抛出 UnsupportedOperationException。

>   Collection 和 Collections区别

1.   Collection是一个集合接口，它提供了对集合对象进行基本操作的通用接口方法，所有集合都是它的子类，比如List、Set等
2.   Collections是一个包装类，包含了很多静态方法、不能被实例化，而是作为工具类使用，比如提供的排序方法： Collections.sort(list)；提供的反转方法：Collections.reverse(list)



<img src="pics/image-20250716230910898.png" alt="image-20250716230910898" style="zoom:40%;" align = "left"/>



## Iterator

Iterator 不能保证迭代的顺序，其顺序完全由**底层集合的特性**决定

Iterator 接口定义了遍历集合的方法，但它的实现则是集合实现类的责任。每个能够返回用于遍历的 Iterator 的集合类都有它自己的 Iterator 实现内部类。这就允许集合类去选择迭代器是 fail-fast 还是 fail-safe 的。

>   Enumeration 和 Iterator接口的区别

Enumeration 的速度是 Iterator 的两倍，也使用更少的内存。Enumeration 是非常基础的，也满足了基础的需要。但是，与 Enumeration 相比，Iterator 更加安全，因当一个集合正在被遍历的时候，它会阻止其它线程去修改集合。 迭代器取代了 Java 集合框架中的 Enumeration。**迭代器允许调用者从集合中移除元素**，而 Enumeration 不能做到。 

>   Iterator 和 ListIterator 的区别

1.   我们可以使用Iterator 来遍历 Set 和 List 集合，而 Listlterator 只能遍历 List
2.   Iterator 只可以向前遍历，而 LIstlterator 可以双向遍历
3.   Listlterator 从 Iterator 接口继承，然后添加了一些额外的功能，比如添加一个元素、替换一个元素、获取前面或后面元素的索引位置。

>   fail-fast和fail-safe选代器的区别是什么？

1.   fail-fast直接在容器上进行，在遍历过程中，一旦发现容器中的数据被修改，就会立刻抛出 **ConcurrentModificationException**异常(避免方式：使用并发集合类，例如CopyOnWriteArrayList)从而导致遍历失败。Collection中所有Iterator的实现都是按照fail-fast来设计的
2.   fail-safe这种遍历基于容器的一个克隆。因此对容器中的内容修改不影响遍历。常见的使用fail-safe 方式遍历的容器有ConcurrentHashMap和CopyOnWriteArrayList。

## List

List (Array ->List : Arrays.asList 使用的是 final 数组，并且不支持add 方法，不支持扩容，不固定的可以使用new ArrayList(Arrays.asList(array))  ;  List -> Array : toArray)

-   ArrayList (数据结构：数组；适用于查询较多；默认大小 JDK1.7之前为10，之后为0，每次扩容1.5)

-   LinkedList (数据结构：双向链表；适用于插入较多;相较于ArrayList消耗更多内存)

-   Vector(线程安全，其大部分方法是直接或间接同步的; 其他实现线程安全需要使用工具类Collections.synchronizedList(new ArrayList()))

>   ArrayList 和 Vector的比较

相同点：

-   两者都是基于索引的，内部由一个数组支持
-   两者维护插入的顺序，我们可以根据插入顺序来获取元素
-   ArrayList 和 Vector 的迭代器实现都是 fail-fast 的
-   ArrayList 和 Vector两者允许 null 值，也可以使用索引值对元素进行随机访问

不同点：

-   Vector 是同步的，而 ArrayList 不是。然而，如果你寻求在迭代的时候对列表进行改变， 你应该使用 CopyOnWriteArrayList
-   ArrayList 比 Vector 快，它因为有同步，不会过载
-   ArrayList 更加通用，因为我们可以使用 Collections工具类轻易地获取同步列表和只读列表。

>   Array 和 ArrayList区别

Array 可以容纳基本类型和对象，而 ArrayList 只能容纳对象

Array 是指定大小的，而 ArrayList 大小是固定的

Array 没有提供 ArrayList 那么多功能，比如 addAll、removeAll 和 iterator 等

Array更加合适的情况：

1.   如果列表的大小已经指定，大部分情况下是存储和遍历它们
2.   对于遍历基本数据类型，尽管 Collections 使用自动装箱来减轻编码任务，在指定大小的基本类型的列表上工作也会变得很慢
3.   如果你要使用多维数组，使用[ ] [ ]比 List<List<>>更容易。

## Map

>   为什么Map接口不继承Collection接口

尽管Map接口和它的实现也是集合框架的一部分，但Map不是集合。Map 包含 key-value 对，它提供抽取 key 或value 列表集合的方法。

>   三个集合视图

-   Keyset()
-   values()
-   entrySet()

都不支持add  和 addAll，支持移除

>   HashMap

JDK8之前底层实现是数组+链表，JDK8改为数组＋链表/红黑树。主要成员变量包括存储数据的table数组、元素数量size、加载因子loadFactor。 

HashMap 中数据以键值对的形式存在，键对应的 hash 值用来计算数组下标，如果两个元素 key 的 hash 值一样，就会发生哈希冲突，被放到同一个链表上。 

table 数组记录 HashMap 的数据，每个下标对应一条链表，所有哈希冲突的数据都会被存放到同一条链表，Node/Entry 节点包含四个成员变量：key、value、next 指针和 hash 值。在JDK8后链表超过8会转化为红黑树。 若当前数据/总数据容量>负载因子，Hashmap将执行扩容操作。 默认初始化容量为16，扩容容量必须是 2的幂次方、最大容量为1<<30、默认加载因子为 0.75。

>   为什么HashMap线程不安全

在JDK1.7中，HashMap采用头插法插入元素，因此并发情况下会导致环形链表，产生死循环。 

虽然JDK1.8采用了尾插法解决了这个问题，但是并发下的put操作也会使前一个key被后一个key覆盖。 

由于HashMap有扩容机制存在，也存在A线程进行扩容后，B线程执行get方法出现失误的情况。

>   HashMap 和 Hashtable的区别

1.   HashMap是Hashtable的轻量级实现，HashMap**允许key和value为nul**l，但最多允许一条记录的key 为null，而HashTable**不允许**。 
2.   HashTable中的方法是线程安全的，而HashMap不是(适合单线程)。在多线程访问HashMap需要提供额外的同步机制。 
3.   Hashtable使用Enumeration进行遍历(不支持fail-fast)，HashMap使用Iterator进行遍历(支持fail-fast)。
4.   Hashtable遍历顺序不可知; 在Java1.4 中引入了 LinkedHashMap, HashMap 的一个子类, 假如你想要遍历顺序，你很容易从 HashMap 转向 LinkedHashMap
5.   HashTable 被认是个遗留的类，如果你寻求在迭代的时候修改 Map，你应该使用 CocurrentHashMap。

>   TreeMap

TreeMap是底层利用红黑树实现的Map结构，底层实现是一棵平衡的排序二叉树，由于红黑树的插入、 删除、遍历时间复杂度都为O(logN)，所以性能上低于哈希表。但是哈希表无法提供键值对的有序输出，红黑树可以按照键的值的大小有序输出。

>   HashMap 还是 TreeMap

如果对Map进行插入、删除或定位一个元素的操作更频繁，HashMap是更好的选择。如果需要对key集合进行有序的遍历，TreeMap是更好的选择。

## Set

Set即集合，该数据结构不允许元素重复且无序。Java对Set有三种实现方式:

-   HashSet 通过 HashMap实现，HashMap 的Key 即 HashSet存储的元素，Value系统自定义一个名为 PRESENT 的 Object 类型常量。判断元素是否相同时，先比较hashCode，相同后再利用equals比较，          查询O(1) 
-   LinkedHashSet继承自 HashSet，通过 LinkedHashMap 实现，使用双向链表维护元素插入顺序。 
-   TreeSet 通过 TreeMap 实现的，底层数据结构是红黑树，添加元素到集合时按照比较规则将其插入合适的位置，保证插入后的集合仍然有序。查询O(logn)

# IO流

>   IO流分类

-   按照流的流向分，可以分为输入流和输出流

-   按照操作单元划分，可以划分为字节流和字符流；
-   按照流的角色划分为节点流和处理流
-   InputStream/Reader：所有的输入流的基类，前者是字节输入流，后者是字符输入
-   OutputStream/Writer：所有输出流的基类，前者是字节输出流，后者是字符输出流

>   BIO. NIO. AIO 的区别

-   BIO:Block 10 同步阻塞式IO，就是我们平常使用的传统IO，它的特点是模式简单使用方便，并发处理能低 
-   NIO: Non 10 同步非阻塞IO，是传统IO的升级，客户端和服务器端通过 **Channel(通道)**通讯，实现了多路复用。 面向缓存
-   AIO: Asynchronous IO 是 NIO 的升级，也叫 NIO2，实现了异步非堵塞IO，异步IO的操作基于**事件和回调机制**

# Java序列化

序列化：将java对象转化为字节序列，由此可以通过网络对象进行传输

反序列化：将字节序列转化为java对象

具体实现：实现Serializable接口，或实现Externalizable接口中的witeExternal() 与readExternal()方法

# Java8

## Lamda表达式

## 方法引用

## 函数式接口

## 默认方法

## stream

## Optional类	

