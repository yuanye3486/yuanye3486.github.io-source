---
title: Java interview Summary
date: 2018-3-8 14:44:19
tags: [java]
categories: [java]
---

> Java 常见知识点与问题总结
> 整理自网络

<!-- more -->

# 基础篇
## Java基础
### 面向对象的特征：抽象、继承、封装和多态  
  1. **抽象**：就是忽略一个主题中与当前目标无关的那些方面，以便更充分地注意与当前目标有关的方面。抽象并不打算了解全部问题，而只是选择其中的一部分，暂时不用部分细节。
  抽象包括两个方面，一是过程抽象，二是数据抽象。
  2. **继承**：是一种联结类的层次模型，并且允许和鼓励类的重用，它提供了一种明确表述共性的方法。对象的一个新类可以从现有的类中派生，这个过程称为类继承。新类继承了原始类的特性，新类称为原始类的派生类（子类），而原始类称为新类的基类（父类）。派生
  类可以从它的基类那里继承方法和实例变量，并且类可以修改或增加新的方法使之更适合特殊的需要。
  3. **封装**：是把过程和数据包围起来，对数据的访问只能通过已定义的界面。面向对象计算始于这个基本概念，即现实世界可以被描绘成一系列完全自治、封装的对象，这些对象通过一个受保护的接口访问其他对象。
  4. **多态性**：是指允许不同类的对象对同一消息作出响应。多态性包括参数化多态性和包含多态性。多态性语言具有灵活、抽象、行为共享、代码共享的优势，很好的解决了应用程序函数同名问题。

### final, finally, finalize 的区别
  - final 用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。
  - finally 是 Java 保证重点代码一定要被执行的一种机制。我们可以使用 try-finally 或者 try-catch-finally 来进行类似关闭 JDBC 连接、保证 unlock 锁等动作
  - finalize 是 Object 类的一个方法，它的设计目的是保证对象在被垃圾收集前完成特定资源的回收。finalize 机制现在已经不推荐使用，并且在 JDK 9 开始被标记为 deprecated。


### Exception、Error、运行时异常与一般异常有何异同
  + **Thorwable**：（表示可抛出）是所有异常和错误的超类，两个直接子类为：
    - **Error**：它是由JVM 产生和抛出的，程序无法处理的错误。这些异常发生时，Java 虚拟机一般会选择线程终止。比如 OutOfMemoryError、ThreadDeath等。
    + **Exception**：是程序本身可以处理的异常，这种异常分两大类运行时异常和非运行时异常。程序中应当尽可能去处理这些异常。
      + **RuntimeException**（运行时异常，又称不检查异常）都是 RuntimeException 类及其子类异常，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生。
        常见运行时异常：
        - NullPointerException
        - IndexOutOfBoundsException
        - ClassCastException
        - NumberFormatException
        - ArrayIndexOutOfBoundsException
      + **非运行时异常**（又称检查异常）是 RuntimeException以外的异常，类型上都属于Exception类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如 IOException、SQLException 等以及用户自定义的 Exception 异常，一般情况下不自定义检查异常。
  - java 异常体系结构图解
    ![异常图解](http://img.blog.csdn.net/20160331115514210)

### ClassNotFoundException 和 NoClassDefFoundError 区别？
  + NoClassDefFoundError
    - 产生原因：
      如果JVM或者ClassLoader实例尝试加载（可以通过正常的方法调用，也可能是使用new来创建新的对象）类的时候却找不到类的定义。要查找的类在编译的时候是存在的，运行的时候却找不到了。这个时候就会导致NoClassDefFoundError。造成该问题的原因可能是打包过程漏掉了部分类，或者jar包出现损坏或者篡改。
    - 解决方法：
      1. 查找那些在开发期间存在于类路径下但在运行期间却不在类路径下的类。
      2. Jar文件的权限问题也可能导致NoClassDefFoundError

  + ClassNotFoundException
    - 产生原因：
      1. Class.forName 方法来动态地加载类
      2. ClassLoader.findSystemClass()
      3. ClassLoader.loadClass()
      当应用程序试图通过类的字符串名称，使用以上三种方法装入类，但却找不到指定名称的类定义时抛出该异常。
    - 解决棒法：
      1. 需要确保所需的类连同它依赖的包存在于类路径中，常见问题在于类名书写错误。

### int 和 Integer 有什么区别，Integer 的值缓存范围
  Java 提供两种不同的类型：引用类型和原始类型（或内置类型）。Int 是 java 的原始数据类型，Integer 是 java 为 int 提供的封装类。
  Java 为每个原始类型提供了封装类，原始类型封装类具体如下：
    boolean Boolean    
    char    Character    
    byte    Byte    
    short   Short    
    int     Integer    
    long    Long    
    float   Float    
    double  Double    
  引用类型和原始类型的行为完全不同，并且它们具有不同的语义。
  引用类型和原始类型具有不同的特征和用法，它们包括：大小和速度问题，这种类型以哪种类型的数据结构存储，当引用类型和原始类型用作某个类的实例数据时所指定的缺省值。
  对象引用实例变量的缺省值为 null，而原始类型实例变量的缺省值与它们的类型有关。

### 包装类，装箱和拆箱
### String、StringBuilder、StringBuffer
### 重载和重写的区别

### 强引用、软引用、弱引用、幻象引用有什么区别？具体使用场景是什么？
  + 强引用
    - 特点：我们平常典型编码Object obj = new Object()中的obj就是强引用。通过关键字new创建的对象所关联的引用就是强引用。 当JVM内存空间不足，JVM宁愿抛出OutOfMemoryError运行时错误（OOM），使程序异常终止，也不会靠随意回收具有强引用的“存活”对象来解决内存不足的问题。对于一个普通的对象，如果没有其他的引用关系，只要超过了引用的作用域或者显式地将相应（强）引用赋值为 null，就是可以被垃圾收集的了，具体回收时机还是要看垃圾收集策略。

  + 软引用
    - 特点：软引用通过SoftReference类实现。 软引用的生命周期比强引用短一些。只有当 JVM 认为内存不足时，才会去试图回收软引用指向的对象：即JVM 会确保在抛出 OutOfMemoryError 之前，清理软引用指向的对象。软引用可以和一个引用队列（ReferenceQueue）联合使用，如果软引用所引用的对象被垃圾回收器回收，Java虚拟机就会把这个软引用加入到与之关联的引用队列中。后续，我们可以调用ReferenceQueue的poll()方法来检查是否有它所关心的对象被回收。如果队列为空，将返回一个null,否则该方法返回队列中前面的一个Reference对象。
    - 应用场景：软引用通常用来实现内存敏感的缓存。如果还有空闲内存，就可以暂时保留缓存，当内存不足时清理掉，这样就保证了使用缓存的同时，不会耗尽内存。

  + 弱引用
    - 弱引用通过WeakReference类实现。 弱引用的生命周期比软引用短。在垃圾回收器线程扫描它所管辖的内存区域的过程中，一旦发现了具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存。由于垃圾回收器是一个优先级很低的线程，因此不一定会很快回收弱引用的对象。弱引用可以和一个引用队列（ReferenceQueue）联合使用，如果弱引用所引用的对象被垃圾回收，Java虚拟机就会把这个弱引用加入到与之关联的引用队列中。
    - 应用场景：弱应用同样可用于内存敏感的缓存。

  + 虚引用
    - 特点：虚引用也叫幻象引用，通过PhantomReference类来实现。无法通过虚引用访问对象的任何属性或函数。幻象引用仅仅是提供了一种确保对象被 finalize 以后，做某些事情的机制。如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。虚引用必须和引用队列 （ReferenceQueue）联合使用。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之关联的引用队列中。
    ReferenceQueue queue = new ReferenceQueue ();
    PhantomReference pr = new PhantomReference (object, queue);
    程序可以通过判断引用队列中是否已经加入了虚引用，来了解被引用的对象是否将要被垃圾回收。如果程序发现某个虚引用已经被加入到引用队列，那么就可以在所引用的对象的内存被回收之前采取一些程序行动。
    - 应用场景：可用来跟踪对象被垃圾回收器回收的活动，当一个虚引用关联的对象被垃圾收集器回收之前会收到一条系统通知。

### 抽象类和接口有什么区别
  - 声明方法的存在而不去实现它的类被叫做抽象类（abstract class），它用于要创建一个体现某些基本行为的类，并为该类声明方法，但不能在该类中实现该类的情况。不能创建 abstract 类的实例。然而可以创建一个变量，其类型是一个抽象类，并让它指向具体子类的一个实例。不能有抽象构造函数或抽象静态方法。
  - Abstract 类的子类为它们父类中的所有抽象方法提供实现，否则它们也是抽象类为。取而代之，在子类中实现该方法。知道其行为的其它类可以在类中实现这些方法。
  - 接口（interface）是抽象类的变体。在接口中，所有方法都是抽象的。多继承性可通过实现这样的接口而获得。接口中的所有方法都是抽象的，没有一个有程序体。接口只可以定义static final成员变量。接口的实现与子类相似，除了该实现类不能从接口定义中继承行为。当类实现特殊接口时，它定义（即将程序体给予）所有这种接口的方法。然后，它可以在实现了该接口的类的任何对象上调用接口的方法。由于有抽象类，它允许使用接口名作为引用变量的类型。通常的动态联编将生效。引用可以转换到接口类型或从接口类型转换，instanceof 运算符可以用来决定某对象的类是否实现了接口。

### 说说反射的用途及实现
  - 反射：用在Java身上指的是我们可以于运行时加载、探知、使用编译期间完全未知的classes。换句话说，Java程序可以加载一个运行时才得知名称的class，获悉其完整构造（但不包括methods定义），并生成其对象实体、或对其fields设值、或唤起其methods。
  - 作用：
    1. 第一个主要作用是获取程序在运行时刻的内部结构。这对于程序的检查工具和调试器来说，是非常实用的功能。
    2. 另外一个作用是在运行时刻对一个Java对象进行操作。 这些操作包括动态创建一个Java类的对象，获取某个域的值以及调用某个方法。在Java源代码中编写的对类和对象的操作，都可以在运行时刻通过反射API来实现。

### 说说自定义注解的场景及实现
  - ![Annotation 思维导图](https://upload-images.jianshu.io/upload_images/3458176-c5642804973c8b6e.jpg?imageMogr2/auto-orient/)
  + Annotation 如何被处理？
    - 当Java源代码被编译时，编译器的一个插件 annotation 处理器则会处理这些 annotation。处理器可以产生报告信息，或者创建附加的Java源文件或资源。如果annotation本身被加上了RententionPolicy的运行时类，则Java编译器则会将annotation的元数据存储到class文件中。然后，Java虚拟机或其他的程序可以查找这些元数据并做相应的处理。

    - 当然除了annotation处理器可以处理annotation外，我们也可以使用反射自己来处理annotation。Java SE 5有一个名为AnnotatedElement的接口，Java的反射对象类Class,Constructor,Field,Method以及Package都实现了这个接口。这个接口用来表示当前运行在Java虚拟机中的被加上了annotation的程序元素。通过这个接口可以使用反射读取annotation。AnnotatedElement接口可以访问被加上RUNTIME标记的annotation，相应的方法有getAnnotation,getAnnotations,isAnnotationPresent。由于Annotation类型被编译和存储在二进制文件中就像class一样，所以可以像查询普通的Java对象一样查询这些方法返回的Annotation。

### HTTP请求的 GET 与 POST 方式的区别

### Session 与 Cookie 区别
  1. Cookie 数据存放在客户的浏览器上，而 Session 数据放在服务器上；
  2. Cookie 分发是通过扩展 HTTP 协议来实现的，服务器通过在 HTTP 的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的 Cookie
  3. Cookie 不是很安全，可以分析存放在本地的 Cookie 并进行 Cookie 欺骗，出于安全考虑应当使用 Session；
  4. Session 会在一定时间内保存在服务器上，当访问增多时会比较影响服务器的性能，出于考虑减轻服务器性能方面，应当使用 Cookie；单个 Cookie 保存的数据不能超过 4K，大多说浏览器都限制了一个站点最多保存 20 个 Cookie。
    个人观点认为将一些登录信息（重要信息）存放在 Session 中，而其他信息如果需要保留，可以放在 Cookie 中

### 列出自己常用的JDK包
  - java.lang
  - java.util
  - java.io

### MVC 设计思想
  - M 即Model(模型层)，主要负责业务逻辑以及数据库的交互
  - V 即View(视图层)，主要用于显示数据和提交数据
  - C 即Controller(控制器)，主要是用作捕获请求并控制请求转发

### equals 与 == 的区别
  == 比较两个对象的引用值是否指相同。
  equals()：根据 equals() 实现的逻辑比较两个对象是否相同（默认实现是通过 == 比较）。

### String 类为什么是 final 的？
  主要考虑到“安全”和“效率”的缘故，若 String 允许被继承，那么它的高度使用率可能会降低程序的性能，因此 String 被定义成了 final。

### String、StringBuffer与StringBuilder的区别？
  java 提供了两个类：String和StringBuffer，java1.5 新增 java.lang.StringBuilder 一个可变的字符序列。
  简单地说，就是一个变量和常量的关系。StringBuffer 对象的内容可以修改；而 String 对象一旦产生后就不可以被修改，重新赋值其实是两个对象。

  StringBuffer
  StringBuffer的内部实现方式和String不同，StringBuffer在进行字符串处理时，不生成新的对象，在内存使用上要优于String类。所以在实际使用时，如果经常需要对一个字符串进行修改，例如插入、删除等操作，使用StringBuffer要更加适合一些。

  String
  在String类中没有用来改变已有字符串中的某个字符的方法，由于不能改变一个java字符串中的某个单独字符，所以在JDK文档中称String类的对象是不可改变的。然而，不可改变的字符串具有一个很大的优点:编译器可以把字符串设为共享的。

  StringBuilder
  StringBuilder 一个可变的字符序列是5.0新增的。此类提供一个与 StringBuffer 兼容的 API，但不保证同步。该类被设计用作 StringBuffer 的一个简易替换，用在字符串缓冲区被单个线程使用的时候（这种情况很普遍）。如果可能，建议优先采用该类，因为在大多数实现中，它比 StringBuffer 要快。两者的方法基本相同。


### 什么是序列化以及用途，什么时候使用序列化？Serializable 接口的作用
  序列化是指把对象转换为字节序列的过程称为对象的序列化；而反序列化是指把字节序列恢复为对象的过程称为对象的反序列化。
  + 对象的序列化主要有两种用途：
    - 把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中。
    - 在网络上传送对象的字节序列。
  + 什么时候使用序列化：
    - 1）对象序列化可以实现分布式对象。主要应用例如：RMI要利用对象序列化运行远程主机上的服务，就像在本地机上运行对象时一样。
    - 2）java对象序列化不仅保留一个对象的数据，而且递归保存对象引用的每个对象的数据。可以将整个对象层次写入字节流中，可以保存在文件中或在网络连接上传递。利用对象序列化可以进行对象的"深复制"，即复制对象本身及引用的对象本身。序列化一个对象可能得到整个对象序列。

### hashCode 和 equals 方法的区别与联系
  在每个覆盖了 equals 方法的类中，也必须覆盖 hashcode 方法。如果不这样做的话，就会违反 Object.hashCode 的通用约定，从而导致该类无法结合所有基于散列的集合一起正常运作，这样的集合包括 HashMap、HashSet 和 Hashtable。
  约定内容如下：
  1. 在应用程序的执行期间，只要对象的 equals 方法的比较操作所用到的信息没有被修改，那么对着同一个对象调用多次，hashCode 方法都必须始终如一地返回同一个整数。在同一个应用程序的多次执行过程中，每次执行所返回的整数可以不一致。
  2. 如果两个对象根据根据 equals(Object) 方法比较是相等的，那么调用这两个对象中任意一个对象的 hashCode 方法都必须产生同样的整数结果。
  3. 如果两个对象根据根据 equals(Object) 方法比较是不相等的，那么调用这两个对象中任意一个对象的 hashCode 方法，则不一定要产生不同的整数结果。

### 为什么Java不支持多重继承?
  1. **简单**。为了强化 Java 简单这个特点，这就是我们去除多重继承的原因。多重继承存在菱形继承问题：有两个类 B 和 C 继承自 A。假设 B 和 C 都继承了 A 的方法并且进行了覆盖，编写了自己的实现。假设 D 通过多重继承继承了 B 和 C，那么 D 应该继承 B 和 C 的重载方法，那么它应该继承哪个的呢？是 B 的还是 C 的呢？
  2. **很少使用**。

### 如何在 Java 中创建 Immutable 对象？
  [总结起来，如果要创建一个“不可变”类，需要遵守下面几条](http://qiusli.github.io/blog/2013/08/08/java-immutable/)：
  1. Class应该定义成final，避免被继承
  2. 将所有成员变量定义为 private 和 final，并且不要实现 setter 方法。
  3. 通常构造对象时，成员变量使用深度拷贝来初始化，而不是直接赋值，这是一种防御措施，因为你无法确定输入对象不被其他人修改。
  4. 如果确实需要实现 getter 方法，或者其他可能会返回内部状态的方法，使用 copy-on-write 原则，创建私有的 copy。

### 单例模式
#### 饱汉模式
  1. 基础饱汉式：核心就是懒加载。好处是更启动速度快、节省资源，一直到实例被第一次访问，才需要初始化单例；小坏处是写起来麻烦，大坏处是线程不安全，if语句存在竞态条件。
    ```java
    public class Singleton1 {
      private static Singleton1 singleton = null;
      private Singleton1() {}
      public static Singleton1 getInstance() {
        if (singleton == null) {
          singleton = new Singleton1();
        }
        return singleton;
      }
    }
    ```
  2. 饱汉–变种1：好处是写起来简单，且绝对线程安全；坏处是并发性能极差，事实上完全退化到了串行。
    ```java
    public class Singleton1_1 {
      private static Singleton1_1 singleton = null;
      private Singleton1_1() {
      }
      public synchronized static Singleton1_1 getInstance() {
        if (singleton == null) {
          singleton = new Singleton1_1();
        }
        return singleton;
      }
    }
    ```
  3. 饱汉–变种2 DCL（双重检查锁）1.0：核心是DCL，看起来变种2似乎已经达到了理想的效果：懒加载+线程安全。可惜的是，正如注释中所说，DCL仍然是线程不安全的，由于指令重排序，你可能会得到“半个对象”。
    ```java
    public class Singleton1_2 {
      private static Singleton1_2 singleton = null;
      private Singleton1_2() {
      }
      public static Singleton1_2 getInstance() {
        // may get half object
        if (singleton == null) {
          synchronized (Singleton1_2.class) {
            if (singleton == null) {
              singleton = new Singleton1_2();
            }
          }
        }
        return singleton;
      }
    }
    ```
    4. 饱汉–变种3 DCL（双重检查锁）2.0：多线程环境下，变种3更适用于性能敏感的场景。但后面我们将了解到，就算是线程安全的，还有一些办法能破坏单例。
      ```java
      public class Singleton1_3 {
        private static volatile Singleton1_3 singleton = null;
        private Singleton1_3() {
        }
        public static Singleton1_3 getInstance() {
          if (singleton == null) {
            synchronized (Singleton1_3.class) {
              // must be a complete instance
              if (singleton == null) {
                singleton = new Singleton1_3();
              }
            }
          }
          return singleton;
        }
      }
      ```
#### 饿汉模式
  好处是天生的线程安全（得益于类加载机制），写起来超级简单，使用时没有延迟；坏处是有可能造成资源浪费（如果类加载后就一直不使用单例的话）。
  ```java
  public class Singleton2 {
    private static final Singleton2 singleton = new Singleton2();
    private Singleton2() {
    }
    public static Singleton2 getInstance() {
      return singleton;
    }
  }
  ```
#### Holder模式
  核心仍然是静态变量，足够方便和线程安全；通过静态的Holder类持有真正实例，间接实现了懒加载。与饱汉的变种3效果相当（略优），都是比较受欢迎的实现方式。同样建议考虑。
  ```java
  public class Singleton3 {
    private static class SingletonHolder {
      private static final Singleton3 singleton = new Singleton3();
      private SingletonHolder() {
      }
    }
    private Singleton3() {
    }
    public synchronized static Singleton3 getInstance() {
      return SingletonHolder.singleton;
    }
  }
  ```
#### 枚举模式
  1. 基础的枚举
  ```java
  // ThreadSafe
  public enum Singleton4 {
    SINGLETON;
  }
  ```


### Java 8 有哪些新特性

## Java常见集合
### [List、Set、Map 的区别](https://blog.csdn.net/qq_22118507/article/details/51576319)
  1. List,Set都是继承自Collection接口，Map则不是
  2. List特点：元素有放入顺序可重复。
     Set特点：元素无放入顺序不可重复，重复元素会覆盖掉，（注意：元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义 equals()方法 ，另外list支持for循环，也就是通过下标来遍历，也可以用迭代器，但是set只能用迭代，因为他无序，无法用下标来取得想要的值。）
  3. List：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。
     Set：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。
  4. Map适合储存键值对的数据
  5. LinkedList、ArrayList、HashSet 是非线程安全的，Vector是线程安全的;
     HashMap 是非线程安全的，HashTable 是线程安全的;
     StringBuilder是非线程安全的，StringBuffer是线程安全的。

### Map
  1. HashMap 就是一张hash表，键和值都没有排序。
  2. TreeMap 以红-黑树结构为基础，键值按顺序排列。
  3. LinkedHashMap 保存了插入时的顺序。
  4. Hashtable 是同步的(而HashMap是不同步的)。所以如果在线程安全的环境下应该多使用HashMap，而不是Hashtable，因为Hashtable对同步有额外的开销。

### HashSet 如何保证不重复
  HashSet中的元素存储在 HashMap中，当向 HashSet add()元素的时，会判断元素是否存在的依据，不仅仅是hash码值就能够确定的，同时还要结合equles方法。

### [HashMap 是线程安全的吗，为什么不是线程安全的（最好画图说明多线程环境下不安全）?](https://www.jianshu.com/p/e2f75c8cce01)
  1. put 的时候导致的多线程数据不一致。
  2. HashMap 的get操作可能因为resize而引起死循环（cpu 100%）
  参考：
  - [JAVA HashMap 的死循环](https://coolshell.cn/articles/9606.html)

### HashMap 的扩容过程
  1. [深入分析ConcurrentHashMap1.8的扩容实现](http://www.importnew.com/23907.html)

### HashMap 1.7 与 1.8 的 区别，1.8 做了哪些优化，如何优化的？
### LinkedHashMap 的应用
### Set 和 hashCode 以及 equals 方法的联系

### Arraylist、LinkedList、Vector 区别

### [HashMap、Hashtable 和 HashSet 的区别](http://www.cnblogs.com/lzrabbit/p/3721067.html#h1)


### HashMap 和 ConcurrentHashMap 的区别
  可参考：[Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析](http://www.importnew.com/28263.html)

### HashMap 的工作原理及代码实现，什么时候用到红黑树

### 多线程情况下 HashMap 死循环的问题

### HashMap 出现 Hash DOS 攻击的问题

### ConcurrentHashMap 的工作原理及代码实现，如何统计所有的元素个数，ConcurrentHashMap的并发度是什么？

### 手写简单的 HashMap

### 数组在内存中如何分配

### 看过那些 Java 集合类的源码

## 进程和线程
### 线程和进程的概念
  - 进程：具有一定独立功能的程序关于某个数据集合上的一次运行活动,进程是系统进行资源分配和调度的一个独立单位。
  - 线程：它是比进程更小的能独立运行的基本单位。线程自己基本上不拥有系统资源,只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源.

### 线程的生命周期，状态是如何转移的？
  + 线程状态
    1. 新建(NEW)：新创建了一个线程对象。
    2. 可运行(RUNNABLE)：线程对象创建后，其他线程(比如 main 线程）调用了该对象的 start() 方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取cpu 的使用权。
    3. 运行(RUNNING)：可运行状态(runnable)的线程获得了cpu 时间片（timeslice） ，执行程序代码。
    4. 阻塞(BLOCKED)：阻塞状态是指线程因为某种原因放弃了cpu 使用权，也即让出了cpu timeslice，暂时停止运行。直到线程进入可运行(runnable)状态，才有机会再次获得cpu timeslice 转到运行(running)状态。
      + 阻塞的情况分三种：
        1. 等待阻塞：运行(running)的线程执行 o.wait() 方法，JVM 会把该线程放入等待队列(waitting queue)中。
        2. 同步阻塞：运行(running)的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则 JVM 会把该线程放入锁池(lock pool)中。
        3. 其他阻塞：运行(running)的线程执行 Thread.sleep(long ms) 或 t.join() 方法，或者发出了 I/O 请求时，JVM 会把该线程置为阻塞状态。当 sleep() 状态超时、join() 等待线程终止或者超时、或者I/O处理完毕时，线程重新转入可运行(runnable)状态。
    5. 死亡(DEAD)：线程run()、main() 方法执行结束，或者因异常退出了run()方法，则该线程结束生命周期。死亡的线程不可再次复生。
  + 状态转换
    ![状态转换图](http://dl.iteye.com/upload/picture/pic/116719/7e76cc17-0ad5-3ff3-954e-1f83463519d1.jpg)
  + 几个方法比较
    1. Thread.sleep(long millis)：一定是当前线程调用此方法，当前线程进入阻塞，但不释放对象锁，millis 后线程自动苏醒进入可运行状态。作用：给其它线程执行机会的最佳方式。
    2. Thread.yield()：一定是当前线程调用此方法，当前线程放弃获取的 cpu 时间片，由运行状态变会可运行状态，让 OS 再次选择线程。作用：让相同优先级的线程轮流执行，但并不保证一定会轮流执行。实际中无法保证 yield() 达到让步目的，因为让步的线程还有可能被线程调度程序再次选中。Thread.yield() 不会导致阻塞。
    3. t.join()/t.join(long millis)：当前线程里调用其它线程1的 join 方法，当前线程阻塞，但不释放对象锁，直到线程1执行完毕或者 millis 时间到，当前线程进入可运行状态。
    4. obj.wait()：当前线程调用对象的 wait() 方法，当前线程释放对象锁，进入等待队列。依靠 notify()/notifyAll() 唤醒或者 wait(long timeout) timeout 时间到自动唤醒。
    5. obj.notify()：唤醒在此对象监视器上等待的单个线程，选择是任意性的。notifyAll() 唤醒在此对象监视器上等待的所有线程。  

### 并行和并发的概念
  - 并行是指两个或者多个事件在同一时刻发生
  - 并发是指两个或多个事件在同一时间间隔发生

### 创建线程的方式及实现
  - 继承 Thread 类
  - 实现 Runnable 接口
  - 使用 Callable 和 Future

### 同步和异步有何异同，在什么情况下分别使用他们？举例说明。
  如果数据将在线程间共享。例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，那么这些数据就是共享数据，必须进行同步存取。
  当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效率。

### 进程间通信的方式？可參考[JAVA线程间通信的几种方式](http://blog.csdn.net/u011514810/article/details/77131296)
  - 通过在线程之间共享对象就可以了，然后通过wait/notify/notifyAll、await/signal/signalAll进行唤起和等待，比方说阻塞队列BlockingQueue就是为线程之间共享数据而设计的

### 线程间通信的方式。可参考[线程间通信剖析](http://www.jasongj.com/java/thread_communication/)

### 为什么需要多线程(多线程的优势)
  1. 更多的计算核心（充分利用硬件资源）
  2. 更快的响应时间
  3. 更好的编程模型

### 什么是线程安全？
  - 如果你的代码在多线程下执行和在单线程下执行永远都能获得一样的结果，那么你的代码就是线程安全的。
  - 线程安全也是有几个级别的
      1. 不可变
        String、Integer、Long 这些，都是final类型的类，它们是不可变类，其对象一定是线程安全的。任何一个线程都改变不了它们的值，要改变除非新创建一个，因此这些不可变对象不需要任何同步手段就可以直接在多线程环境下使用
      2. 绝对线程安全
        不管运行时环境如何，调用者都不需要额外的同步措施。要做到这一点通常需要付出许多额外的代价，Java中标注自己是线程安全的类，实际上绝大多数都不是线程安全的，不过绝对线程安全的类，Java中也有，比方说CopyOnWriteArrayList、CopyOnWriteArraySet
      3. 相对线程安全
        相对线程安全也就是我们通常意义上所说的线程安全，像Vector这种，add、remove方法都是原子操作，不会被打断，但也仅限于此，如果有个线程在遍历某个 Vector、有个线程同时在 add 这个 Vector，99% 的情况下都会出现 ConcurrentModificationException，也就是 fail-fast 机制。
      4. 线程非安全
        如：ArrayList、LinkedList、HashMap等都是线程非安全的类    

### 如何保证线程安全？
  - 什么是线程安全？
    定义：当多个线程访问某个类时，这个类始终都能表现出正确的行为，那么就称这个类是线程安全的。
    线程安全性的定义中，最核心的概念就是正确性。
    正确性的含义是某个类的行为与其规范完全一致。
  - 为什么会出现线程不安全？
    因为存在有限的共享资源（可变的共享变量），以及多线程的并发访问。
  + 如何实现线程安全？
    + 互斥同步：是常见的一种并发正确性保障手段。
      - 同步：是指在多个线程并发访问共享数据时，保证共享数据在同一时刻只被一个（或者是一些，使用信号量的时候）线程使用。
      - 同步互斥，在这四个字里面：互斥是因，同步是果；互斥是方法，同步是目的。
      - Java中基本的互斥同步手段就是 synchronized 关键字，除此之外，还可以使用 java.util.concurrent(J.U.C)包中的重入锁（ReentrantLock）来实现同步。
      - 其最主要的问题就是进行线程阻塞和唤醒所带来的性能问题，因此这种同步也称为阻塞同步。
      - 互斥同步属于一种悲观的并发策略
    + 非阻塞同步
      - 它是一种基于冲突检测的乐观并发策略，通俗的讲就是先进行操作，如果没有其他线程争用共享数据，那操作就成功了；如果共享数据有争用，产生了冲突，那就采用其他的补偿措施（最常见的就是不断重试，直到成功为止），这种乐观策略的许多实现都不需要把线程挂起，因此这种同步操作称为非阻塞同步。
      - 乐观并发策略需要“硬件指令集的发展”才能进行，因为我们需要操作和冲突检测这两个步骤具备原子性，原子性的保证需要靠硬件来完成。
      - CAS 指令需要有3个操作数，内存地址（V）、旧的预期值（A）和新值（B），CAS指令执行时，当且仅当V符合旧预期值A时，处理器用新值B更新V的值，否则它就不执行跟新。
    + 无同步方案
      要保证线程安全，并不是一定就要进行同步，同步只是保证共享数据争用时的正确性的手段，如果一个方法本来就不涉及共享数据，那他自然就无须任何同步措施去保证正确性。因此会有一些代码天生就是线程安全的：
      - 可重入代码：都是线程安全的。
        判断原则：如果一个方法，他的返回结果是可以预测的，只要输入了相同的数据，就都能返回相同的结果，那他就满足可重入性的要求。
      - 线程本地存储
        如果一段代码中所需要的数据必须与其它代码共享，并且这些共享数据的代码能够保证在同一个线程中执行，这样无需同步也能保证线程之间不出现数据争用的问题。
        实例：如果经典Web交互模型中的“一个请求对应一个服务器线程”的处理方式。


    - 不在线程之间共享状态变量
    - 将状态变量修改为不可变的变量
    + 在访问状态变量时使用同步
      - 加锁
        1. 锁能使其保护的代码以串行的形式来访问，当给一个复合操作加锁后，能使其成为原子操作。一种错误的思想是只要对写数据的方法加锁，其实这是错的，对数据进行操作的所有方法都需加锁，不管是读还是写。
        2. 加锁时需要考虑性能问题，不能总是一味地给整个方法加锁synchronized就了事了，应该将方法中不影响共享状态且执行时间比较长的代码分离出去。
        3. 加锁的含义不仅仅局限于互斥，还包括可见性。为了确保所有线程都能看见最新值，读操作和写操作必须使用同样的锁对象。
      - CAS 算法
      + volatile
        - volatile：写内存语义是直接刷新到主内存中，读的内存语义是直接从主内存中读取。
        - volatile 内存语义实现原理
            对于一般的变量则会被重排序，而对于volatile则不能，这样会影响其内存语义，所以为了实现volatile的内存语义JMM会限制重排序。

### 什么是 CAS，CAS 有什么缺陷，如何解决？
  比较并交换(compare and swap, CAS)，是原子操作的一种，可用于在多线程编程中实现不被打断的数据交换操作，从而避免多线程同时改写某一数据时由于执行顺序不确定性以及中断的不可预知性产生的数据不一致问题。CAS操作基于CPU提供的原子操作指令实现，各个编译器根据这个特点实现了各自的原子操作函数。
  简单说：CAS需要检查操作值有没有发生改变，如果没有发生改变则更新。
  - 优点：无锁；非阻塞
  - 缺点：
    1. 循环时间太长
      如果CAS一直不成功呢？这种情况绝对有可能发生，如果自旋CAS长时间地不成功，则会给CPU带来非常大的开销。在JUC中有些地方就限制了CAS自旋的次数，例如BlockingQueue的SynchronousQueue。
    2. 只能保证一个共享变量的原子操作（当然如果你有办法把多个变量整成一个变量，利用CAS也不错。例如读写锁中state的高地位）
    3. 存在 ABA问题
      - 概念：如果一个值原来是A，变成了B，然后又变成了A，那么在CAS检查的时候会发现没有改变，但是实质上它已经发生了改变，这就是所谓的ABA问题。
      - 解决：AtomicStampedReference 它可以通过控制变量值的版本来保证CAS的正确性，从而避免ABA问题。
      - 引申：Java concurrent 并发包依赖于 CAS 算法，既然 CAS算法存在 ABA 问题，那是不是 AtomicInteger 等根本就不能用了呢？
        肯定是可以用的，AtomicInteger处理的一个数值，所有就算出现ABA问题问题，也不会有什么影响；但是如果这里是一个地址（地址被重用是很经常发生的，一个内存分配后释放了，再分配，很有可能还是原来的地址），比较地址发现没有问题，但其实这个对象早就变了，这时候就可以使用AtomicStampedReference来解决ABA问题。

### 说说 CountDownLatch, CyclicBarrier, Semaphore 原理和区别
  + 概念
    - CountDownLatch：是一个同步工具类，它允许一个或多个线程一直等待，直到其他线程的操作执行完后再执行。
    - CyclicBarrier： 它可以实现让一组线程等待至某个状态之后再全部同时执行。
    - Semaphore（默认非公平）：是一种基于计数的信号量。它可以设定一个阈值，基于此，多个线程竞争获取许可信号，做完自己的申请后归还，超过阈值后，线程申请许可信号将会被阻塞。
  + 原理
    - CountDownLatch 是通过一个计数器来实现的，计数器的初始值为线程的数量。每当一个线程完成了自己的任务后，计数器的值就会减1。当计数器值到达0时，它表示所有的线程已经完成了任务，然后在闭锁上等待的线程就可以恢复执行任务。
    - CyclicBarrier 内部定义了一个Lock对象，每当一个线程调用CyclicBarrier的await方法时，将剩余拦截的线程数减1，然后判断剩余拦截数是否为0，如果不是，进入Lock对象的条件队列等待。如果是，执行barrierAction对象的Runnable方法，然后将锁的条件队列中的所有线程放入锁等待队列中，这些线程会依次的获取锁、释放锁，接着先从await方法返回，再从CyclicBarrier的await方法中返回。
  + 应用场景
    - CountDownLatch
      1. 实现最大的并行性
        有时我们想同时启动多个线程，实现最大程度的并行性。例如，我们想测试一个单例类。如果我们创建一个初始计数为1的CountDownLatch，并让所有线程都在这个锁上等待，那么我们可以很轻松地完成测试。我们只需调用 一次countDown()方法就可以让所有的等待线程同时恢复执行。
      2. 开始执行前等待n个线程完成各自任务：例如应用程序启动类要确保在处理用户请求前，所有N个外部系统已经启动和运行了。
    - CyclicBarrier
      可以用于多线程计算数据,最后合并计算结果的场景  
    - Semaphore
      1. 可以用来构建一些对象池，资源池之类的，比如数据库连接池。
      2. 也可以创建计数为 1 的 Semaphore，将其作为一种类似互斥锁的机制
  + 区别
    - CountDownLatch 一般用于某个线程A等待若干个其他线程执行完任务之后，它才执行。
    - CyclicBarrier 一般用于一组线程互相等待至某个状态，然后这一组线程再同时执行
    - Semaphore 其实和锁有点类似，它一般用于控制对某组资源的访问权限
    - 实际上可以通过 CountDownLatch 的 countDown() 和 await() 来实现 CyclicBarrier 的功能。即 CountDownLatch 中的 countDown() + await() = CyclicBarrier 中的 await()。注意：在一个线程中先调用countDown()，然后调用await()。

### 说说 Exchanger 原理
  - Exchanger（交换者）是一个用于线程间协作的工具类。Exchanger 用于进行线程间的数据交换。它提供一个同步点，在这个同步点两个线程可以交换彼此的数据。这两个线程通过 exchange 方法交换数据，如果第一个线程先执行 exchange 方法，它会一直等待第二个线程也执行 exchange，当两个线程都到达同步点时，这两个线程就可以交换数据，将本线程生产出来的数据传递给对方。
  - 使用场景：Exchanger 也可以用于校对工作

### ThreadLocal 原理分析，ThreadLocal 为什么会出现 OOM，出现的深层次原理？
  + 原理：每个Thread 维护一个 ThreadLocalMap 映射表，这个映射表的 key 是 ThreadLocal实例本身，value 是真正需要存储的 Object。
    1. ThreadLocal 本身并不存储值，它只是作为一个 key 来让线程从 ThreadLocalMap 获取 value。
    2. ThreadLocalMap 是使用 ThreadLocal 的弱引用作为 Key 的，弱引用的对象在 GC 时会被回收。
  - 作用：提供线程内的局部变量，这种变量在线程的生命周期内起作用，减少同一个线程内多个函数或者组件之间一些公共变量的传递的复杂度。  
    ThreadLocal的使用不是为了能让多个线程共同使用某一对象，而是我有一个线程A，其中我需要用到某个对象o，这个对象o在这个线程A之内会被多处调用，而我不希望将这个对象o当作参数在多个方法之间传递，于是，我将这个对象o放到TheadLocal中，这样，在这个线程A之内的任何地方，只要线程A之中的方法不修改这个对象o，我都能取到同样的这个变量o。
  - 与普通变量的区别：每个使用该变量的线程都会初始化一个完全独立的实例副本。ThreadLocal 变量通常被 private static 修饰。当一个线程结束时，它所使用的所有 ThreadLocal 相对的实例副本都可被回收。
  + 为什么会内存泄漏？
    1. ThreadLocalMap 使用 ThreadLocal 的弱引用作为 key，如果一个 ThreadLocal 没有外部强引用来引用它，那么系统 GC 时，这个 ThreadLocal 会被回收，ThreadLocalMap 中就会出现 key 为 null 的 Entry，就没有办法访问这些 key 为 null 的 Entry 的 value。如果当前线程再迟迟不结束的话，这些 key 为 null 的 Entry 的 value 就会一直存在一条强引用链：Thread Ref -> Thread -> ThreaLocalMap -> Entry -> value 永远无法回收，造成内存泄漏。
    2. ThreadLocalMap 的设计已经考虑到上述情况，也加了一些防护措施：在ThreadLocal 的 get()，set()，remove() 时都会清除线程 ThreadLocalMap 里所有 key 为 null 的 value。
    3. 但上述预防措施并不能保证不会内存泄漏：
      - 使用 static 的 ThreadLocal，延长了 ThreadLocal 的生命周期，可能导致的内存泄漏。
      - 分配使用了 ThreadLocal 又不再调用 get()，set()，remove() 方法，那么就会导致内存泄漏。
  + 如何避免内存泄漏？
    每次使用完 ThreadLocal，都调用它的 remove() 方法，清除数据。
  - 适用场景：
    1. ThreadLocal 适用于变量在线程间隔离且在方法间共享的场景

  - 可参考：
    1. [正确理解 ThreadLocal 的原理与适用场景](http://www.jasongj.com/java/threadlocal/)
    2. [深入分析 ThreadLocal 内存泄漏问题](http://www.importnew.com/22039.html)

### [Java中 Object.wait() Thread.sleep() Thread.yield() 方法的区别？](https://www.jianshu.com/p/25e959037eed)
  + wait() 和 sleep() 的区别：
    1. wait()和sleep()的关键的区别在于，wait()是用于线程间通信的，而sleep()是用于短时间暂停当前线程。
    2. 更加明显的一个区别在于，当一个线程调用wait()方法的时候，会释放它持有的锁，但是调用sleep()方法的时候，不会释放他所持有的锁。
    3. wait只能在同步（synchronize）环境中被调用，而sleep不需要。
    4. 进入wait状态的线程能够被notify和notifyAll线程唤醒，但是进入sleeping状态的线程不能被notify方法唤醒。
    5. wait通常有条件地执行，线程会一直处于wait状态，直到某个条件变为真。但是sleep仅仅让你的线程进入睡眠状态。
    6. wait方法在进入wait状态的时候会释放对象的锁，但是sleep方法不会。
    7. wait方法是针对一个被同步代码块加锁的对象，而sleep是针对一个线程。
  + yield() 和 sleep() 的区别：
    1. yield方法会临时暂停当前正在执行的线程，来让有同样优先级的正在等待的线程有机会执行。如果没有正在等待的线程，或者所有正在等待的线程的优先级都比较低，那么该线程会继续运行。执行了yield方法的线程什么时候会继续运行由线程调度器来决定，不同的厂商可能有不同的行为。yield方法不保证当前的线程会暂停或者停止，但是可以保证当前线程在调用yield方法时会放弃CPU。
    2. Thread.sleep() 方法用来暂停线程的执行，将CPU放给线程调度器。
    3. Thread.sleep() 方法是一个静态方法，它暂停的是当前执行的线程。
    4. Java有两种sleep方法，一个只有一个毫秒参数，另一个有毫秒和纳秒两个参数。
    5. 与wait方法不同，sleep方法不会释放锁
    6. 如果其他的线程中断了一个休眠的线程，sleep方法会抛出Interrupted Exception。
    7. 休眠的线程在唤醒之后不保证能获取到CPU，它会先进入就绪态，与其他线程竞争CPU。

### 使用 wait() 和 notify() 实现生产者与消费者问题
  ```java
  import java.util.LinkedList;
  import java.util.Queue;

  public class ProducerAndConsumer {
      private static final int MAX_SIZE = 10;
      private static Queue<Integer> productQueue = new LinkedList<>();
      private static int productId;

      public static void main(String[] args) {
          // 生产者
          new Thread(() -> {
              while (true) {
                  synchronized (productQueue) {
                      while (productQueue.size() == MAX_SIZE) {
                          try {
                              productQueue.wait();
                          } catch (InterruptedException e) {
                              e.printStackTrace();
                          }
                      }
                      productQueue.add(++productId);
                      System.out.println("生产产品：" + productId + ", 产品数量：" + productQueue.size());
                      productQueue.notifyAll();
                  }
              }
          }).start();

          // 消费者
          new Thread(() -> {
              while (true) {
                  synchronized (productQueue) {
                      while (productQueue.isEmpty()) {
                          try {
                              productQueue.wait();
                          } catch (InterruptedException e) {
                              e.printStackTrace();
                          }
                      }
                      System.out.println("消费产品：" + productQueue.poll() + ", 产品数量：" + productQueue.size());
                      productQueue.notifyAll();
                  }
              }
          }).start();
      }
  }
  ```

### 为什么wait()，notify() 和 notifyAll() 必须在同步块或同步方法中调用？
  简而言之，我们从同步块或者同步方法中调用wait()，notify()和notifyAll()方法可以避免：
  - IllegalMonitorStateException，如果我们不通过同步环境（synchronized context）调用这几个方法，系统将抛出此异常
  - wait()和notify()之间任何潜在的竞争条件。

### java-为什么wait，notify和notifyall定义在Object中
  1. wait和nofity不是常见的普通java方法或同步工具，在Java中它们更多的是实现两个线程之间的通信机制。 如果不能通过类似synchronized这样的Java关键字来实现这种机制，那么Object类中就是定义它们最好的地方，以此来使任何Java对象都可以拥有实现线程通信机制的能力。记住synchronized和wait,notify是两个不同的问题域，并且不要混淆它们的相似或相关性。 同步类似竞态条件，是提供线程间互斥和确保Java类的线程安全性的，而wait和notify是两个线程之间的通信机制。
  2. 每个对象都可以作为锁，这是另一个原因wait和notify在Object类中声明，而不是Thread类。
  3. 在Java中，为了进入临界区代码段，线程需要获得锁并且它们等待锁可用，它们不知道哪些线程持有锁而它们只知道锁是由某个线程保持，它们应该等待锁而不是知道哪个线程在同步块内并要求它们释放锁。 这个比喻适合等待和通知在object类而不是Java中的线程。
  这些只是我的想法为什么wait和notify方法在Object类中声明，而不是Java中的Thread，当然你可以有不同的观点。 在现实中，它就是Java不支持操作符重载一样，只是Java设计者做的一个设计决定。

### 讲讲线程池的实现原理
### 线程池的几种实现方式
  + ThreadPoolExecutor 构造函数
    ```java
    public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        // 这几个参数都是必须要有的
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();

        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
    ```
    - corePoolSize
    - maximumPoolSize：​最大线程数，线程池允许创建的最大线程数。
    - workQueue：任务队列，BlockingQueue 接口的某个实现（常使用 ArrayBlockingQueue 和 LinkedBlockingQueue）。
    - keepAliveTime：空闲线程的保活时间，如果某线程的空闲时间超过这个值都没有任务给它做，那么可以被关闭了。注意这个值并不会对所有线程起作用，如果线程池中的线程数少于等于核心线程数 corePoolSize，那么这些线程不会因为空闲太长时间而被关闭，当然，也可以通过调用 allowCoreThreadTimeOut(true)使核心线程数内的线程也可以被回收。
    - threadFactory：用于生成线程，一般我们可以用默认的就可以了。通常，我们可以通过它将我们的线程的名字设置得比较可读一些，如 Message-Thread-1， Message-Thread-2 类似这样。
    - handler：当线程池已经满了，但是又有新的任务提交的时候，该采取什么策略由这个来指定。有几种方式可供选择，像抛出异常、直接拒绝然后返回等，也可以自己实现相应的接口实现自己的逻辑。
  + 线程池中的线程创建时机
    1. 如果当前线程数少于 corePoolSize，那么提交任务的时候创建一个新的线程，并由这个线程执行这个任务；
    2. 如果当前线程数已经达到 corePoolSize，那么将提交的任务添加到队列中，等待线程池中的线程去队列中取任务；
    3. 如果队列已满，那么创建新的线程来执行任务，需要保证池中的线程数不会超过 maximumPoolSize，如果此时线程数超过了 maximumPoolSize，那么执行拒绝策略。
    4. 如果将队列设置为无界队列，那么线程数达到 corePoolSize 后，其实线程数就不会再增长了。

### Java中的同步集合与并发集合有什么区别？
### 线程池的种类，区别和使用场景？

### 分析线程池的实现原理和线程的调度过程？

### 常用的线程池模式以及不同线程池的使用场景

### 线程池如何调优，最大数目如何确认？

### 数据连接池的工作机制是什么？
  J2EE 服务器启动时会建立一定数量的池连接，并一直维持不少于此数目的池连接。客户端程序需要连接时，池驱动程序会返回一个未使用的池连接并将其表记为忙。如果当前没有空闲连接，池驱动程序就新建一定数量的连接，新建连接的数量由配置参数决定。当使用的池连接调用完成后，池驱动程序将此连接表记为空闲，其他调用就可以使用这个连接。

### ExecutorService你⼀般是怎么⽤的？是每个service放⼀个还是⼀个项⽬ ⾥⾯放⼀个？有什么好处？
### 线程池内的线程如果全部忙，提交⼀个新的任务，会发⽣什么？队列全部 塞满了之后，还是忙，再提交会发⽣什么？
### 写出3条你遵循的多线程最佳实践

### 可参考：
  1. [Java多线程编程核心技术](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484881&idx=2&sn=b0ecf85cd7c9e543c84e7a9859c20a26)
  2. [40个Java多线程问题总结](http://www.importnew.com/18459.html)
  3. [Java 并发基础之内存模型](https://javadoop.com/post/java-memory-model)

## 锁机制
### 什么是锁？
  锁是保证并发共享数据一致性的工具

### 什么是死锁？
  如果一个进程集合里面的每个进程都在等待这个集合中的其他一个进程（包括自身）才能继续往下执行，若无外力他们将无法推进，这种情况就是死锁，处于死锁状态的进程称为死锁进程。

### 产生死锁的四个条件
  1. 互斥：进程对所分配到的资源不允许其他进程进行访问，若其他进程访问该资源，只能等待，直至占有该资源的进程使用完成后释放该资源
  2. 请求与保持：进程获得一定的资源之后，又对其他资源发出请求，但是该资源可能被其他进程占有，此事请求阻塞，但又对自己获得的资源保持不放
  3. 不剥夺：指进程已获得的资源，在未完成使用之前，不可被剥夺，只能在使用完后自己释放
  4. 循环等待：指进程发生死锁后，必然存在一个进程和资源之间的环形链

### 处理死锁的基本方法
  1. 预防死锁：通过设置一些限制条件，去破坏产生死锁的必要条件
  2. 避免死锁：在资源分配过程中，使用某种方法避免系统进入不安全的状态，从而避免发生死锁
  3. 检测死锁：允许死锁的发生，但是通过系统的检测之后，采取一些措施，将死锁清除掉
  4. 解除死锁：该方法与检测死锁配合使用

### Java 中常见的锁有哪些？
  + 阻塞锁
    - 概念：可以说是让线程进入阻塞状态进行等待，当获得相应的信号（唤醒，时间）时，才可以进入线程的准备就绪状态，准备就绪状态的所有线程，通过竞争，进入运行状态。
  + 按照锁性质分类：
    + 公平锁 / 非公平锁
      + 公平锁：指多个线程按照申请锁的顺序来获取锁。
        - ReentrantLock 可通过构造函数指定为公平锁
      + 非公平锁：指多个线程获取锁的顺序并不是按照申请锁的顺序，有可能后申请的线程比先申请的线程优先获取锁。有可能，会造成优先级反转或者饥饿现象。
        - 实现：ReentrantLock（默认为非公平锁）；Synchronized
        - 优点：吞吐量比公平锁大
    + 独享锁 / 共享锁
      + 独享锁：指该锁一次只能被一个线程持有。如：ReentrantLock；ReentrantReadWriteLock.WriteLock；Synchronized
      + 共享锁：指该锁可被多个线程持有。如：ReentrantReadWriteLock.ReadLock
    + 互斥锁 / 读写锁
      上面讲的独享锁/共享锁就是一种广义的说法，互斥锁/读写锁就是具体的实现。
      互斥锁在Java中的具体实现就是ReentrantLock
      读写锁在Java中的具体实现就是ReadWriteLock
    + 悲观锁 / 乐观锁
      + 乐观锁与悲观锁不是指具体的什么类型的锁，而是指看待并发同步的角度。
        - 悲观锁认为对于同一个数据的并发操作，一定是会发生修改的，哪怕没有修改，也会认为修改。因此对于同一个数据的并发操作，悲观锁采取加锁的形式。悲观的认为，不加锁的并发操作一定会出问题。
        - 乐观锁则认为对于同一个数据的并发操作，是不会发生修改的。在更新数据的时候，会采用尝试更新，不断重新的方式更新数据。乐观的认为，不加锁的并发操作是没有事情的。
      + 适用场景：
        - 悲观锁适合写操作非常多的场景
        - 乐观锁适合读操作非常多的场景，不加锁会带来大量的性能提升
      + 实现：
        - 悲观锁在Java中的使用，就是利用各种锁。
        - 乐观锁在Java中的使用，是无锁编程，常常采用的是CAS算法，典型的例子就是原子类，通过CAS自旋实现原子操作的更新。
    + 可重入锁  
      - 可重入锁又名递归锁，是指在同一个线程在外层方法获取锁的时候，在进入内层方法会自动获取锁。
      - jdk里面没有默认的不可重入锁实现类.
      - 实现：ReentrantLock；Synchronized
      - 优点：可一定程度避免死锁
  + 按照设计方案分类：
    + [自旋锁](http://ifeve.com/java_lock_see1/)
      - 概念：自旋锁是采用让当前线程不停地的在循环体内执行实现的，当循环的条件被其他线程改变时 才能进入临界区。
      - 适用场景：适合于线程竞争不激烈，且锁保持时间短。
        因为自旋锁只是将当前线程不停地执行循环体，不进行线程状态的改变，所以响应速度更快。但当线程数不停增加时，性能下降明显，因为每个线程都需要执行，占用CPU时间。
    + 锁粗化 / 锁消除
      - **锁粗化**：如果虚拟机探测到有这样一串零碎的操作都对同一个对象加锁，将会把加锁同步的范围扩展到整个操作序列的外部，这样就只需要加锁一次就够了。
      - **锁消除**：指虚拟机即时编译器在运行时，对一些代码上要求同步，但是被检测到不可能存在共享数据竞争的锁进行消除。锁消除主要判定依据来源于逃逸分析的数据支持。锁消除是在编译器级别的事情。
    + 偏向锁 / 轻量级锁 / 重量级锁
      这三种锁是指锁的状态，并且是针对 Synchronized。在Java 5通过引入锁升级的机制来实现高效Synchronized。这三种锁的状态是通过对象监视器在对象头中的字段来表明的。
      - **偏向锁**：指一段同步代码一直被一个线程所访问，那么该线程会自动获取锁。降低获取锁的代价。
      - **轻量级锁**：指当锁是偏向锁的时候，被另一个线程所访问，偏向锁就会升级为轻量级锁，其他线程会通过自旋的形式尝试获取锁，不会阻塞，提高性能。
      - **重量级锁**：指当锁为轻量级锁的时候，另一个线程虽然是自旋，但自旋不会一直持续下去，当自旋一定次数的时候，还没有获取到锁，就会进入阻塞，该锁膨胀为重量级锁。重量级锁会让其他申请的线程进入阻塞，性能降低。
      - 锁升级是单向的: 无锁 -> 偏向锁 -> 轻量级锁 -> 重量级锁
    + 分段锁
      - 分段锁其实是一种锁的设计，并不是具体的一种锁。
      - 分段锁的设计目的是细化锁的粒度，当操作不需要更新整个数组的时候，就仅仅针对数组中的一项进行加锁操作。
      - 示例：
          以 ConcurrentHashMap 来说一下分段锁的含义以及设计思想，ConcurrentHashMap 中的分段锁称为 Segment，它即类似于 HashMap（JDK7与JDK8中HashMap的实现）的结构，即内部拥有一个 Entry 数组，数组中的每个元素又是一个链表；同时又是一个 ReentrantLock（Segment继承了ReentrantLock)。
          当需要put元素的时候，并不是对整个hashmap进行加锁，而是先通过hashcode来知道他要放在那一个分段中，然后对这个分段进行加锁，所以当多线程put的时候，只要不是放在一个分段中，就实现了真正的并行的插入。
          但是，在统计size的时候，可就是获取hashmap全局信息的时候，就需要获取所有的分段锁才能统计。
  - 方法锁 / 对象锁 / 类锁
  - 线程锁
  - 信号量
  + 可参考：
    1. [JAVA锁有哪些种类](http://blog.csdn.net/nalanmingdian/article/details/77800355)
    2. [JAVA锁有哪些种类，以及区别](https://www.cnblogs.com/lxmyhappy/p/7380073.html)

### Condition
### 重入锁的概念，重入锁为什么可以防止死锁

### 如何检查死锁（通过jConsole检查死锁）

### volatile 实现原理（禁止指令重排、刷新内存）？
  - 作用：内存可见性和禁止指令重排序。
  - volatile 如何解决内存可见性：读一个 volatile 变量之前，需要先使相应的本地缓存失效，这样就必须到主内存读取最新值，写一个 volatile 属性会立即刷入到主内存。
  - volatile 适用场景：某个属性被多个线程共享，其中有一个线程修改了此属性，其他线程可以立即得到修改后的值。在并发包的源码中，它使用得非常多。
  - volatile 属性的读写操作都是无锁的，它不能替代 synchronized，因为它没有提供原子性和互斥性。因为无锁，不需要花费时间在获取锁和释放锁上，所以说它是低成本的。
  - volatile 只能作用于属性，我们用 volatile 修饰属性，这样 compilers 就不会对这个属性做指令重排序。
  - volatile 提供了可见性，任何一个线程对其的修改将立马对其他线程可见。volatile 属性不会被线程缓存，始终从主存中读取。
  - volatile 提供了 happens-before 保证，对 volatile 变量 v 的写入 happens-before 所有其他线程后续对 v 的读操作。
  - volatile 可以使得 long 和 double 的赋值是原子的。

### 什么时候需要加 volatile 关键字？它能保证线程安全吗？
  volatile 的适用场景：适合用于单线程写，多线程读数据的场合。
  volatile 可以及时把变量的修改写入主存，每个线程读取值的时候都必须从主存读取，这样做保证了可见性，但其安全性在多线程环境并不能获得保证。

### volatile 和 synchronized 比较
  1. volatile 是线程同步的轻量级实现，所以 volatile 性能肯定比synchronized要好，并且 volatile 只能修饰变量，而synchronized可以修饰方法，以及代码块。
  2. 多线程访问 volatile 不会发生堵塞，而 synchronized 可能会出现堵塞。
  3. volatile 保证数据的可见性，但不能保证原子性；而 synchronized 可以保证原子性，也可以间接保证可见性，因为它会将私有内存和公共内存中的数据做了同步。
  4. volatile 解决的是变量在多个线程之间的可见性；而 synchronized 解决的是多个线程之间访问资源的同步性。

### synchronized 实现原理（对象监视器）
  每个对象有一个监视器锁（monitor），当 monitor 被占用时就会处于锁定状态。线程释放锁时其必须是对应的 monitor 的所有者。
  + 线程尝试获取 monitor 所有权的过程如下：
    1. 如果 monitor 的进入数为 0，则该线程进入 monitor，然后将进入数设置为 1，该线程即为 monitor 的所有者。
    2. 如果线程已经占有该 monitor，只是重新进入，则进入 monitor 的进入数加 1。
    3. 如果其他线程已经占用了 monitor，则该线程进入阻塞状态，直到 monitor 的进入数为 0，再重新尝试获取 monitor 的所有权。
  + 线程释放锁的过程如下：
    线程释放锁时 monitor 的进入数减 1，如果减 1 后进入数为 0，那线程退出 monitor，不再是这个 monitor 的所有者。其他被这个 monitor 阻塞的线程可以尝试去获取这个 monitor 的所有权。

### synchronized 与 lock 的区别
  Java 提供了两种锁机制：synchronized 和 lock。
  + 用法区别
    - synchronized：可以加在方法，特定代码块中
    - lock：需要显示指定起始位置和终止位置；且在加锁和解锁处需要通过lock()和unlock()显示指出。
  + 性能区别
    - synchronized 是托管给 JVM 执行的，而 lock 是 java 写的控制锁的代码。
    - synchronize 在 Java1.5及之前的版本中性能是低效的，比 Lock 锁效率要低，因为这是一个重量级操作。
    - synchronize 在 Java1.6进行了很多优化，引入了自旋锁，锁消除，锁粗化，轻量级锁，偏向锁等等，性能得到改善并不比 Lock 差。
    + 实现机制不同：
      - synchronized 原始采用的是CPU悲观锁机制，即线程获得的是独占锁。独占锁意味着其他线程只能依靠阻塞来等待线程释放锁。而在CPU转换线程阻塞时会引起线程上下文切换，当有很多线程竞争锁的时候，会引起CPU频繁的上下文切换导致效率很低。
      - Lock 用的是乐观锁方式。所谓乐观锁就是，每次不加锁而是假设没有冲突而去完成某项操作，如果因为冲突失败就重试，直到成功为止。乐观锁实现的机制就是CAS操作。
  + 用途区别
    synchronized 原语和 ReentrantLock 在一般情况下没有什么区别，但是在非常复杂的同步应用中，请考虑使用ReentrantLock，特别是遇到如下情况时：
    1. 某个线程在等待一个锁的控制权的这段时间需要中断。
    2. 需要分开处理一些 wait-notify，ReentrantLock 里面的 Condition 应用，能够控制 notify 哪个线程。
    3. 具有公平锁功能，每个到来的线程都将排队等候。

### synchronized 和 ReentrantLock 有什么不同？
  + 用法上的不同：
    - synchronized 既可以加在方法上，也可以加载特定代码块上，而 lock 需要显示地指定起始位置和终止位置。
    - synchronized 是托管给 JVM 执行的，lock 的锁定是通过代码实现的，它有比 synchronized 更精确的线程语义。
  + 性能上的不同：
    - lock 接口的实现类 ReentrantLock，不仅具有和 synchronized 相同的并发性和内存语义，还多了锁投票、定时锁、等候和中断锁等。
    - 在竞争不是很激烈的情况下，synchronized 的性能优于 ReentrantLock，竞争激烈的情况下 synchronized 的性能会下降的非常快，而 ReentrantLock 则基本不变。
  + 锁机制不同：
    - synchronized 获取锁和释放锁的方式都是在块结构中，当获取多个锁时，必须以相反的顺序释放，并且是自动解锁。而 Lock 则需要开发人员手动释放，并且必须在 finally 中释放，否则会引起死锁。

### 线程中断的两种情况
  - 当线程处于阻塞状态或者试图执行一个阻塞操作时，我们可以使用线程实例方法interrupt()进行线程中断，执行中断操作后将会抛出 InterruptException 异常(该异常必须捕捉无法向外抛出)并将中断状态复位。
  - 当线程处于运行状态时，我们也可调用线程实例方法 interrupt() 进行线程中断，但同时必须手动判断中断状态，并编写中断线程的代码(其实就是结束run方法体的代码)。

### synchronized 关键字锁住的是什么东⻄？在字节码中是怎么表示的？在内存中的对象上表现为什么？
### wait/notify/notifyAll ⽅法需不需要被包含在 synchronized 块中？这是为什么？
### 除了synchronized 关键字之外，你是怎么来保障线程安全的？    
### 多个线程同时读写，读线程的数量远远⼤于写线程，你认为应该如何解决并发的问题？你会选择加什么样的锁？

### 可参考：[Java多线程编程核心技术](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484881&idx=2&sn=b0ecf85cd7c9e543c84e7a9859c20a26)

## JUC
### Java 并发体系思维导图
  ![Java 并发体系思维导图](http://cmsblogs.com/wp-content/images/share/chenssy_juc_201712.png)

### JAVA 的 AQS 是否了解，它是⼲嘛的？

### LockSupport 工具

### Condition 接口及其实现原理

### Fork/Join 框架的理解

### 分段锁的原理,锁力度减小的思考

### 八种阻塞队列以及各个阻塞队列的特性
### [Java中的队列都有哪些，有什么区别？](https://mp.weixin.qq.com/s?__biz=MzAwMTE3MDY4MQ==&mid=2652433302&idx=1&sn=2c51d1990fbdd2c917bc3cdc00508a72)
### 常见的原子操作类
### Java 8并法包下常见的并发类


## JVM
  - JVM 思维导图
    ![JVM 思维导图](http://fakerblog-wordpress.stor.sinaapp.com/uploads/2014/07/1232.jpg)

  + JVM 运行时内存区域划分

### [java内存区域划分、硬件内存架构、java 内存模型（JMM）区别](https://blog.csdn.net/javazejian/article/details/72772461#%E7%90%86%E8%A7%A3java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F%E4%B8%8Ejava%E5%86%85%E5%AD%98%E6%A8%A1%E5%9E%8B)
  + java内存区域划分
    1. **程序计数器**(Program Counter Register)
      用来指示 执行哪条指令的
    2. **Java 栈**(VM Stack)或称 Java 虚拟机栈
      - Java栈是Java方法执行的内存模型
      + Java栈中存放的是一个个的栈帧，每个栈帧对应一个被调用的方法。
        在栈帧中包括：
          - 局部变量表(Local Variables)
          - 操作数栈(Operand Stack)
          - 指向当前方法所属的类的运行时常量池（运行时常量池的概念在方法区部分会谈到）的引用(Reference to runtime constant pool)
          - 方法返回地址(Return Address)
          - 一些额外的附加信息
    3. **本地方法栈**(Native Method Stack)
    4. **方法区**(Method Area)  
      存储了每个类的信息（包括类的名称、方法信息、字段信息）、静态变量、常量以及编译器编译后的代码等。
    5. **堆**(Heap)
      堆是用来存储对象本身以及数组（当然，数组引用是存放在Java栈中的）的。
  + java内存模型
    1. JMM本身是一种抽象的概念，并不真实存在，它描述的是一组规则或规范，通过这组规范定义了程序中各个变量（包括实例字段，静态字段和构成数组对象的元素）的访问方式。
    2. JMM与Java内存区域的划分是不同的概念层次。
    3. 更恰当说JMM描述的是一组规则，通过这组规则控制程序中各个变量在共享数据区域和私有数据区域的访问方式。
    4. JMM是围绕原子性、有序性、可见性展开的。
    5. JMM与Java内存区域唯一相似点，都存在共享数据区域和私有数据区域，在JMM中主内存属于共享数据区域，从某个程度上讲应该包括了堆和方法区，而工作内存数据线程私有数据区域，从某个程度上讲则应该包括程序计数器、虚拟机栈以及本地方法栈。或许在某些地方，我们可能会看见主内存被描述为堆内存，工作内存被称为线程栈，实际上他们表达的都是同一个含义。
  + 硬件内存架构
    1. ![硬件内存架构](https://img-blog.csdn.net/20170611211802727?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvamF2YXplamlhbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    2. 多线程的执行最终都会映射到硬件处理器上进行执行。
    3. Java内存模型和硬件内存架构并不完全一致。对于硬件内存来说只有寄存器、缓存内存、主内存的概念，并没有工作内存(线程私有数据区域)和主内存(堆内存)之分，也就是说Java内存模型对内存的划分对硬件内存并没有任何影响，因为JMM只是一种抽象的概念，是一组规则，并不实际存在，不管是工作内存的数据还是主内存的数据，对于计算机硬件来说都会存储在计算机主内存中，当然也有可能存储到CPU缓存或者寄存器中，因此总体上来说，Java内存模型和计算机硬件内存架构是一个相互交叉的关系，是一种抽象概念划分与真实物理硬件的交叉。(注意对于Java内存区域划分也是同样的道理)


### 如何理解并发的三个特性（问题）：原子性、内存可见性、有序性？
  + 原子性：
    - 原子性是指不可再分的最小操作指令，即单条机器指令，原子性操作任意时刻只能有一个线程，因此是线程安全的。
    - 即使是在多线程环境下，一个操作一旦开始就不会被其他线程影响。比如对于一个静态变量int x，两条线程同时对他赋值，线程A赋值为1，而线程B赋值为2，不管线程如何运行，最终x的值要么是1，要么是2，线程A和线程B间的操作是没有干扰的，这就是原子性操作，不可被中断的特点。
  + 内存可见性：指当多个线程并发访问共享变量时，一个线程对共享变量的修改，其它线程能够立即看到。
     - 如果所有的属性都使用了 final 修饰，那么 volatile 也是可以不要的，这就是 final 带来的可见性影响。
     - 在对象的构造方法中设置 final 属性，同时在对象初始化完成前，不要将此对象的引用写入到其他线程可以访问到的地方（不要让引用在构造函数中逸出）。如果这个条件满足，当其他线程看到这个对象的时候，那个线程始终可以看到正确初始化后的对象的 final 属性。
  + 有序性
    - 有序性是指在单线程环境下代码的执行是按顺序依次执行的，但对于多线程环境，则可能出现乱序现象，因为程序编译成机器码指令后可能会出现指令重排现象，重排后的指令与原指令的顺序未必一致。
    - 以下机制可能会引起重排序：
      1. 编译器优化的重排：对于没有数据依赖关系的操作，编译器在编译的过程中会进行一定程度的重排。
      2. 指令并行的重排：CPU 优化行为，也是会对不存在数据依赖关系的指令进行一定程度的重排。
      3. 内存系统的重排序：内存系统没有重排序，但是由于有缓存的存在，使得程序整体上会表现出乱序的行为。

### 如何理解 JMM 中的 happens-before 原则？
  倘若在程序开发中，仅靠sychronized和volatile关键字来保证原子性、可见性以及有序性，那么编写并发程序可能会显得十分麻烦，幸运的是，在Java内存模型中，还提供了happens-before 原则来辅助保证程序执行的原子性、可见性以及有序性的问题，它是判断数据是否存在竞争、线程是否安全的依据，happens-before 原则内容如下：
  - 程序顺序原则，即在一个线程内必须保证语义串行性，也就是说按照代码顺序执行。
  - 锁规则 解锁(unlock)操作必然发生在后续的同一个锁的加锁(lock)之前，也就是说，如果对于一个锁解锁后，再加锁，那么加锁的动作必须在解锁动作之后(同一个锁)。
  - volatile规则 volatile变量的写，先发生于读，这保证了volatile变量的可见性，简单的理解就是，volatile变量在每次被线程访问时，都强迫从主内存中读该变量的值，而当该变量发生变化时，又会强迫将最新的值刷新到主内存，任何时刻，不同的线程总是能够看到该变量的最新值。
  - 线程启动规则 线程的start()方法先于它的每一个动作，即如果线程A在执行线程B的start方法之前修改了共享变量的值，那么当线程B执行start方法时，线程A对共享变量的修改对线程B可见
  - 传递性 A先于B ，B先于C 那么A必然先于C
  - 线程终止规则 线程的所有操作先于线程的终结，Thread.join()方法的作用是等待当前执行的线程终止。假设在线程B终止之前，修改了共享变量，线程A从线程B的join方法成功返回后，线程B对共享变量的修改将对线程A可见。
  - 线程中断规则 对线程 interrupt()方法的调用先行发生于被中断线程的代码检测到中断事件的发生，可以通过Thread.interrupted()方法检测线程是否中断。
  - 对象终结规则 对象的构造函数执行，结束先于finalize()方法

### JMM 如何解决原子性、内存可见性、有序性问题？
  + 原子性问题
    - JVM自身提供了对基本数据类型读写操作的原子性
    - 对于方法或代码块级别的原子性操作，可以使用 synchronized 关键字或者重入锁(ReentrantLock)保证程序执行的原子性。
  + 可见性问题
    - 对由于工作内存与主内存同步延迟现象导致的可见性问题，可以使用 synchronized 或 volatile 关键字解决，它们都可以使一个线程修改后的变量立即对其他线程可见。
  + 有序性问题
    - 对于指令重排导致的可见性问题和有序性问题，则可以利用volatile关键字解决，因为volatile的另外一个作用就是禁止重排序优化。
  JMM内部还定义一套happens-before 原则来保证多线程环境下两个操作间的原子性、可见性以及有序性。

### volatile内存语义
  volatile 是 Java 虚拟机提供的轻量级的同步机制。volatile关键字有如下两个作用：
  - 保证被volatile修饰的共享变量对所有线程总是可见的，也就是当一个线程修改了一个被volatile修饰共享变量的值，新值总是可以被其他线程立即得知。
  - 禁止指令重排序优化
### JMM 如何实现让 volatile 变量对其他线程立即可见？
  当写一个 volatile 变量时，JMM 会把该线程对应的工作内存中的共享变量值刷新到主内存中，当读取一个 volatile 变量时，JMM 会把该线程对应的工作内存置为无效，那么该线程将只能从主内存中重新读取共享变量。volatile 变量正是通过这种写-读方式实现对其他线程可见（但其内存语义实现则是通过内存屏障）。

### 什么是类的加载
  - 类的加载是指将类的.class文件中的二进制数据读入到内存中，将其放在运行时数据区的方法区内，然后在堆区创建一个java.lang.Class对象，用来封装类在方法区内的数据结构。
  - 类加载的最终产品是位于堆区中的 Class 对象，Class 对象封装了类在方法区内的数据结构，并且向 Java 程序员提供了访问方法区内的数据结构的接口。
### class 文件加载方式
  - 从本地系统中直接加载
  - 通过网络下载.class文件
  - 从zip，jar等归档文件中加载.class文件
  - 从专有数据库中提取.class文件
  - 将Java源文件动态编译为.class文件
### 类加载器
  + 从 JVM 角度只有两种类加载器：
    - 启动类加载器：是虚拟机自身的一部分，使用 C++ 实现。
    - 所有其他的类加载器：全继承自 java.lang.ClassLoader，这些类加载器需要由启动类加载器加载到内存中之后才能去加载其他的类。由 Java 实现。
  + 从 Java 开发人员的角度，类加载器分三类：
    1. **启动类加载器**：Bootstrap ClassLoader，负责加载存放在JDK\\jre\\lib(JDK代表JDK的安装目录，下同)下，或被 -Xbootclasspath 参数指定的路径中的，并且能被虚拟机识别的类库（如rt.jar，所有的java.\*开头的类均被Bootstrap ClassLoader加载）。启动类加载器是无法被Java程序直接引用的。
    2. **扩展类加载器**：Extension ClassLoader，该加载器由 sun.misc.Launcher$ExtClassLoader 实现，它负责加载 JDK\\jre\\lib\\ext 目录中，或者由 java.ext.dirs 系统变量指定的路径中的所有类库（如javax.\*开头的类），开发者可以直接使用扩展类加载器。
    3. **应用程序类加载器**：Application ClassLoader，该类加载器由 sun.misc.Launcher$AppClassLoader 来实现，它负责加载用户类路径（ClassPath）所指定的类，开发者可以直接使用该类加载器，如果应用程序中没有自定义过自己的类加载器，一般情况下这个就是程序中默认的类加载器。
### 类的生命周期
  + 加载：查找并加载类的二进制数据，在 Java 堆中也创建一个 java.lang.Class 类的对象
    - 类加载的时机：类加载器并不需要等到某个类被“首次主动使用”时再加载它，JVM规范允许类加载器在预料某个类将要被使用时就预先加载它，如果在预先加载的过程中遇到了.class 文件缺失或存在错误，类加载器必须在程序首次主动使用该类时才报告错误（LinkageError错误）如果这个类一直没有被程序主动使用，那么类加载器就不会报告错误
  + 连接
    又包含三块内容：
    - 验证：文件格式、元数据、字节码、符号引用验证。确保被加载的类的正确性。
    - 准备：为类的静态变量分配内存，并将其初始化为默认值
    - 解析：把类中的符号引用转换为直接引用
  + 初始化：为类的静态变量赋予正确的初始值
    + 类初始化时机：只有当对类的主动使用的时候才会导致类的初始化，类的主动使用包括以下六种：
      - 创建类的实例，也就是 new 的方式
      - 访问某个类或接口的静态变量，或者对该静态变量赋值
      - 调用类的静态方法
      - 反射（如Class.forName(“com.mysql.jdbc.Driver”)）
      - 初始化某个类的子类，则其父类也会被初始化
      - Java虚拟机启动时被标明为启动类的类（Java Test），直接使用java.exe命令来运行某个主类
  - 使用：new 出对象，程序中使用
  - 卸载：执行垃圾回收
### JVM 类加载机制
  + **父类委托**：先让父类加载器试图加载该类，只有在父类加载器无法加载该类时才尝试从自己的类路径中加载该类
    + 双亲委派模型工作流程：
      如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把请求委托给父加载器去完成，依次向上，因此，所有的类加载请求最终都应该被传递到顶层的启动类加载器中，只有当父加载器在它的搜索范围中没有找到所需的类时，即无法完成该加载，子加载器才会尝试自己去加载该类。
    + 双亲委派模型意义：
      - 系统类防止内存中出现多份同样的字节码
      - 保证Java程序安全稳定运行
  - **全盘负责**：当一个类加载器负责加载某个 Class 时，该 Class 所依赖的和引用的其他Class也将由该类加载器负责载入，除非显示使用另外一个类加载器来载入
  - **缓存机制**：缓存机制将会保证所有加载过的 Class 都会被缓存，当程序中需要使用某个 Class 时，类加载器先从缓存区寻找该 Class，只有缓存区不存在，系统才会读取该类对应的二进制数据，并将其转换成 Class 对象，存入缓存区。这就是为什么修改了 Class 后，必须重启 JVM，程序的修改才会生效。

### JAVA 类加载器包括⼏种？它们之间的⽗⼦关系是怎么样的？双亲委派机制是什么意思？有什么好处？

### 你知道哪些或者你们线上使⽤什么 GC 策略? 它有什么优势，适⽤于什么场景？
### 堆内存设置的参数是什么？
### Perm Space中保存什么数据? 会引起OutOfMemory吗？ 6. 做gc时，⼀个对象在内存各个Space中被移动的顺序是什么？
### Java1.8 之后 Perm Space 有哪些变动？MetaSpace ⼤⼩默认是⽆限的么？还是你们会通过什么⽅式来指定⼤⼩？
### 如何⾃定义⼀个类加载器？你使⽤过哪些或者你在什么场景下需要⼀个⾃ 定义的类加载器吗？
### Jstack 是⼲什么的？Jstat呢？如果线上程序周期性地出现卡顿，你怀疑可能是 GC 导致的，你会怎么来排查这个问题？线程⽇志⼀般你会看其中的什么部分？
### StackOverFlow 异常有没有遇到过？⼀般你猜测会在什么情况下被触 发？如何指定⼀个线程的堆栈⼤⼩？⼀般你们写多少？

### 什么时候发生 GC。
  Java 中的堆是 GC 的主要区域。GC 分为两种：Minor GC、FullGC (或称为 Major GC)。
  Minor GC 是发生在新生代中的垃圾收集动作，所采用的是复制算法。
  Full GC 是发生在老年代的垃圾收集动作，所采用的是标记-清除算法。
  + Minor GC(Young GC)
    - 从年轻代空间（包括 Eden 和 Survivor 区域）回收内存被称为 Minor GC
    - 当 JVM 无法为一个新的对象分配空间时会触发 Minor GC，比如当 Eden 区满了。所以分配率越高，越频繁执行 Minor GC。
    - Minor GC 都会触发“全世界的暂停（stop-the-world）”
    - 执行 Minor GC 操作时，不会影响到永久代
    + 触发条件：当Eden区满时，触发 Minor GC。

  + Full GC：清理整个堆空间—包括年轻代和老年代
    + 触发条件：
      1. 调用System.gc时，系统建议执行Full GC，但是不必然执行
      2. 老年代空间不足
      3. 方法去空间不足
      4. 通过Minor GC后进入老年代的平均大小大于老年代的可用内存
      5. 由Eden区、From Space区向To Space区复制时，对象大小大于To Space可用内存，则把该对象转存到老年代，且老年代的可用内存小于该对象大小

  + 堆大小 = 新生代 + 老年代
    JDK1.6 默认：新生代(Young)与老年代(Old)的比例为 1:2 (该值可以通过参数 –XX:NewRatio 来指定)
    JDK1.6 默认：Edem : from : to(from) = 8 : 1 : 1 (可以通过参数 –XX:SurvivorRatio 来设定)
    JVM 每次只会使用 Eden 和其中的一块 Survivor 区域来为对象服务，所以无论什么时候，总是有一块 Survivor 区域是空闲着的。

### Minor GC 过程
  1. 对象出生在 Eden (或一个 Survivor 区域，这里假设是 from 区域)
  2. 经一次 Minor GC 后，若对象还活着，且能够被另外一块 Survivor 区域所容纳(这里为 to 区域，即 to 区域有足够的内存空间来存储 Eden 和 from 区域中存活的对象)，则使用复制算法将这些仍然还存活的对象复制到另外一块 Survivor 区域 (即 to 区域) 中
  3. 然后清理所使用过的 Eden 以及 Survivor 区域 ( 即from 区域 )，并且将这些对象的年龄设置为 1，以后对象在 Survivor 区每熬过一次 Minor GC，就将对象的年龄 + 1。
  4. 当对象的年龄达到某个值时 ( 默认是 15 岁，可以通过参数 -XX:MaxTenuringThreshold 来设定)，这些对象就会成为老年代。但这也不是一定的，对于一些较大的对象 ( 即需要分配一块较大的连续内存空间 ) 则是直接进入到老年代。

### Java 中会存在内存泄漏吗？
  会。有两类主要的Java内存泄漏：
  - **非必要的对象引用**
    Java代码常常保留对于不再需要的对象引用，这阻止了垃圾收集器对这部分对象的回收工作。Java对象通常被其他对象包含引用，为此一个单一对象可以保持整个对象树在内存中，于是导致了如下问题:
      1. 在向数组添加对象以后遗漏了对于他们的处理
      2. 直到你再次使用对象的时候都不释放引用。比如一个菜单指令可以插件一个对象实例引用并且不释放便于以后再次调用的时候使用，但是也许永远不会发生。
      3. 在其他引用依然需要旧有状态的时候贸然修改对象状态。比如当你为了在一个文本文件里面保存一些属性而使用一个数组，诸如"字符个数"等字段在不再需要的时候依然保留在内存当中.
      4. 允许一个长久执行的线程所引用的对象。设置引用为 NULL 也无济于事，在线程退出和空闲之前，对象不会被收集释放
  - **未释放的系统资源**
    Java方法可以定位 Java 实例以外的堆内存，诸如针对视窗和位图的内存资源。Java常常通过JNI(Java Native Interface)调用C/C++子程序定位这些资源。


### 内存溢出 OOM 和堆栈溢出 SOE 的示例及原因、如何排查与解决
### 如何判断对象是否可以回收或存活
### 常见的GC回收算法及其含义
### 常见的JVM性能监控和故障处理工具类：jps、jstat、jmap、jinfo、jconsole等
### JVM如何设置参数
### JVM性能调优
### 可参考：
  1. [深入理解 Java 内存模型读书笔记](http://www.54tianzhisheng.cn/2018/02/28/Java-Memory-Model/)
  2. [jvm知识点总览](http://www.ityouknow.com/java/2017/03/01/jvm-overview.html)
  3. [java类的加载机制](http://www.cnblogs.com/ityouknow/p/5603287.html)


## 设计模式
### 常见的设计模式
### 设计模式的的六大原则及其含义
### 常见的单例模式以及各种实现方式的优缺点，哪一种最好，手写常见的单利模式
### 设计模式在实际场景中的应用
### Spring 中用到了哪些设计模式
### MyBatis 中用到了哪些设计模式
### 你项目中有使用哪些设计模式
### 说说常用开源框架中设计模式使用分析
### 动态代理很重要！！！

## 数据结构
### 树（二叉查找树、平衡二叉树、红黑树、B树、B+树）
### 深度有限算法、广度优先算法
### 克鲁斯卡尔算法、普林母算法、迪克拉斯算法
### 什么是一致性Hash及其原理、Hash环问题
### [常见的排序算法和查找算法：快排、折半查找、堆排序等](https://itimetraveler.github.io/2017/07/18/%E5%85%AB%E5%A4%A7%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E6%80%BB%E7%BB%93%E4%B8%8Ejava%E5%AE%9E%E7%8E%B0/)

## 网络 / IO 基础
### BIO、NIO、AIO的概念
  可参考：[Java NIO浅析](https://tech.meituan.com/nio.html)
### 什么是长连接和短连接
### Http1.0 和 2.0 相比有什么区别，可参考[Http 2.0](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484611&idx=1&sn=66c875392eedff8150633ddcd5d83e7a)
### Https的基本概念
### 三次握手和四次挥手、为什么挥手需要四次
### 从游览器中输入URL到页面加载的发生了什么？可参考[从输入URL到页面加载发生了什么](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483724&idx=1&sn=e58dd30d124971c795584e8673d6cc71)

# 数据存储和消息队列

## 数据库
### MySQL 存储引擎区别
  MySQL 5.5 之前版本默认的存储引擎为 MyISAM，从5.5之后为 InnoDB。
  + MyISAM
    - 不支持事务，但是每次查询都是原子的。
    - 支持表级锁，即每次操作是对整个表加锁；
    - 存储表的总行数；
    - 一个MYISAM表有三个文件：索引文件、表结构文件、数据文件；
    - 采用菲聚集索引，索引文件的数据域存储指向数据文件的指针。辅索引与主索引基本一致，但是辅索引不用保证唯一性。
  + InnoDB
    - 支持ACID的事务，支持事务的四种隔离级别；
    - 支持行级锁及外键约束：因此可以支持写并发；
    - 不存储总行数；
    - 一个InnoDb引擎存储在一个文件空间（共享表空间，表大小不受操作系统控制，一个表可能分布在多个文件里），也有可能为多个（设置为独立表空，表大小受操作系统文件大小限制，一般为2G），受操作系统文件大小的限制；
    - 主键索引采用聚集索引（索引的数据域存储数据文件本身），辅索引的数据域存储主键的值；因此从辅索引查找数据，需要先通过辅索引找到主键值，再访问辅索引；最好使用自增主键，防止插入数据时，为维持B+树结构，文件的大调整。
  + Memory
  ...
### MySQL 索引定义
  官方定义：索引（Index）是帮助MySQL高效获取数据的数据结构。所以索引的本质：索引是数据结构。

### MySQL 索引类型
  + BTree 索引（B-tree：又称B树、B-树，又叫平衡(balance)多路查找树）
    - B-Tree
      1. MyISAM使用B-Tree实现主键索引、非主键索引和唯一索引。
    - B+Tree
      1. InnoDB 索引使用的是B+Tree。
  + 哈希索引
    - hash 就是一种（key=>value）形式的键值对，目前仅 Memory 引擎支持。
    - 由于hash索引可以一次定位，不需要像树形索引那样逐层查找,因此具有极高的效率
  + 空间数据索引（R-Tree）
    - 仅支持geometry数据类型
    - 相对于BTREE，RTREE 的优势在于范围查找.
  + 全文索引
    仅 MyISAM 引擎支持

### 为什么使用 B+Tree 作为索引
  - B+树更适合外部存储,由于内节点无 data 域,一个结点可以存储更多的内结点,每个节点能索引的范围更大更精确,也意味着 B+树单次磁盘IO的信息量大于B-树,I/O效率更高。
  - Mysql是一种关系型数据库，区间访问是常见的一种情况，B+树叶节点增加的链指针,加强了区间访问性，可使用在范围区间查询等，而B-树每个节点 key 和 data 在一起，则无法区间查找。    

### MySQL BTree 索引和 Hash 索引的区别
  - Hash 索引仅能满足"=","IN"和"<=>"查询，不能使用范围查询。
    由于 Hash 索引比较的是进行 Hash 运算之后的 Hash 值，所以它只能用于等值的过滤，不能用于基于范围的过滤，因为经过相应的 Hash 算法处理之后的 Hash 值的大小关系，并不能保证和Hash运算前完全一样。
  - Hash 索引无法被用来避免数据的排序操作。
    由于 Hash 索引中存放的是经过 Hash 计算之后的 Hash 值，而Hash值的大小关系并不一定和 Hash 运算前的键值完全一样，所以数据库无法利用索引的数据来避免任何排序运算；
  - Hash 索引不能利用部分索引键查询（仅对使用全部索引键查询有效）。
    对于组合索引，Hash 索引在计算 Hash 值的时候是组合索引键合并后再一起计算 Hash 值，而不是单独计算 Hash 值，所以通过组合索引的前面一个或几个索引键进行查询的时候，Hash 索引也无法被利用。
  - Hash 索引在任何时候都不能避免表扫描。
    前面已经知道，Hash 索引是将索引键通过 Hash 运算之后，将 Hash运算结果的 Hash 值和所对应的行指针信息存放于一个 Hash 表中，由于不同索引键存在相同 Hash 值，所以即使取满足某个 Hash 键值的数据的记录条数，也无法从 Hash 索引中直接完成查询，还是要通过访问表中的实际数据进行相应的比较，并得到相应的结果。
  - Hash 索引遇到大量Hash值相等的情况后性能并不一定就会比B-Tree索引高。
    对于选择性比较低的索引键，如果创建 Hash 索引，那么将会存在大量记录指针信息存于同一个 Hash 值相关联。这样要定位某一条记录时就会非常麻烦，会浪费多次表数据的访问，而造成整体性能低下。

### MySQL 索引使用的注意事项

### MySQL 悲观锁和乐观锁
  - 悲观锁：假设会发生并发冲突，回避一切可能违反数据完整性的操作。
    在一般情况下，悲观锁依靠数据库的锁机制实现，以保证操作最大程度的排他性和独占性，因而会导致数据库性能的大量开销和并发性很低，特别是对长事务而言，这种开销往往过于巨大而无法承受。
  - 乐观锁：假设不会发生并发冲突，只在提交操作时检查是否违反数据完整性，注意乐观锁并不能解决脏读的问题(关于脏读稍后解析)。
    乐观锁，大多情况下是基于数据版本（ Version ）记录机制实现。

### DDL、DML、DCL分别指什么
  - DDL：data manipulation language 数据操纵语言
    主要用来对数据库的数据进行一些操作，如： SELECT、UPDATE、INSERT、DELETE。
  - DML：data definition language 数据库定义语言
    如：CREATE、ALTER、DROP等
  - DCL：Data Control Language 数据库控制语言
    用来设置或更改数据库用户或角色权限的语句，如 grant,deny,revoke等语句

### explain 命令
### left join，right join，inner join
### 数据库事物 ACID
  （原子性、一致性、隔离性、持久性）
### 事务的隔离级别
  （读未提交、读以提交、可重复读、可序列化读）
### 脏读、幻读、不可重复读
### 数据库的几大范式
### 数据库常见的命令
### 说说分库与分表设计
### 分库与分表带来的分布式困境与应对之策（如何解决分布式下的分库分表，全局表？）
### 说说 SQL 优化之道。可参考[19个MySQL性能优化要点解析](http://blog.csdn.net/xlgen157387/article/details/50735269)
### MySQL遇到的死锁问题、如何排查与解决
### 存储引擎的 InnoDB与MyISAM区别，优缺点，使用场景
### 索引类别（B+树索引、全文索引、哈希索引）、索引的原理
### 什么是自适应哈希索引（AHI）
### 为什么要用 B+tree 作为MySQL索引的数据结构
### 聚集索引与非聚集索引的区别
### 遇到过索引失效的情况没，什么时候可能会出现，如何解决
### limit 20000 加载很慢怎么解决
### 如何选择合适的分布式主键方案
### 选择合适的数据存储方案
### 常见的几种分布式ID的设计方案
### 常见的数据库优化方案，在你的项目中数据库如何进行优化的
### 如果有很多数据插⼊MYSQL 你会选择什么⽅式?

### 如果查询很慢，你会想到的第⼀个⽅式是什么？索引是⼲嘛的?

### 如果建了⼀个单列索引，查询的时候查出2列，会⽤到这个单列索引吗？

### 如果建了⼀个包含多个列的索引，查询的时候只⽤了第⼀列，能不能⽤上 这个索引？查三列呢？

### 接上题，如果where条件后⾯带有⼀个 i + 5 < 100 会使⽤到这个索引吗？

### 怎么看是否⽤到了某个索引？

### like %aaa%会使⽤索引吗? like aaa%呢?

### drop、truncate、delete的区别？

### 平时你们是怎么监控数据库的? 慢 SQL 是怎么排查的？

### 你们数据库是否⽀持emoji表情，如果不⽀持，如何操作?

### 你们的数据库单表数据量是多少？⼀般多⼤的时候开始出现查询性能急 剧下降？

### 查询死掉了，想要找出执⾏的查询进程⽤什么命令？找出来之后⼀般你 会⼲嘛？

### 读写分离是怎么做的？你认为中间件会怎么来操作？这样操作跟事务有 什么关系？ 14. 分库分表有没有做过？线上的迁移过程是怎么样的？如何确定数据是正 确的？

### MySQL常用命令

### 数据库中事物的特征？

### JDBC的使用？

### MySQL为什么使用B+树作为索引？


## Redis
### Redis与Memorycache的区别？
### Redis的五种数据结构？
  - string（字符串）
  - Hash（哈希表）
  - List（列表）
  - Set（集合）
  - SortedSet（有序集合）
    基于跳跃表（skip list）实现

### 渐进式rehash过程？
### rehash源码？
### 持久化机制
### reaof源码？
### 事务与事件
### 主从复制
### 启动过程
### 集群
### Redis的6种数据淘汰策略
### redis的并发竞争问题？
### Redis 有哪些数据类型，可参考[Redis常见的5种不同的数据类型详解](https://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483987&idx=1&sn=5c5e4cd5bc73a7e6f84e5d6adfab0935)
### Redis 内部结构
### Redis 使用场景

### Redis 持久化机制
  + 快照持久化
    - 快照就是我们所说的备份。用户可以将Redis内存中的数据在某一个时间点进行备份，在创建快照之后，用户可以对快照进行备份。
    - 创建快照的方式，并不能完全保证我们的数据不丢失
    - 客户端通过向Redis发送BGSAVE 命令来创建快照。
    - 客户端通过向Redis发送SAVE 命令来创建快照。
  + AOF 持久化
    - AOF持久化会将被执行的写命令写到AOF文件的末尾，以此来记录数据发生的变化。这样，我们在恢复数据的时候，只需要从头到尾的执行一下AOF文件即可恢复数据。


  可参考[使用快照和AOF将Redis数据持久化到硬盘中](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483992&idx=1&sn=8f554bc490c4db1a78a30144f873e911)

### Redis 集群方案与实现
### Redis 为什么是单线程的？
### 缓存雪崩、缓存穿透、缓存预热、缓存更新、缓存降级
### 使用缓存的合理性问题
### Redis 常见的回收策略

## 消息队列
  MQ 是一个互联网架构中常见的解耦利器
  ![消息队列思维导图](http://neoremind.com/wp-content/uploads/MQ_mind2.png)
### 消息队列的使用场景
  + 什么时候使用 MQ？
    - 数据驱动的任务依赖
    - 上游不关心多下游执行结果
      上游需要关注执行结果时要用“调用”，上游不关注执行结果时，就可以使用MQ了。
    - 上游关注执行结果，但执行时间很长（异步返回执行时间长）
      有时候上游需要关注执行结果，但执行结果时间很长（典型的是调用离线处理，或者跨公网调用），也经常使用回调网关+MQ来解耦。
  + 什么时候不使用 MQ？
    - 上游实时关注执行结果

### 消息的重发补偿解决思路
### 消息的幂等性解决思路
### 消息的堆积解决思路
### 自己如何实现消息队列
### 如何保证消息的有序性
### 可参考：
  - [到底什么时候该使用 MQ？](https://mp.weixin.qq.com/s?__biz=MjM5ODYxMDA5OQ==&mid=2651960012&idx=1&sn=c6af5c79ecead98daa4d742e5ad20ce5)
  - [消息队列技术点梳理（思维导图版）](http://neoremind.com/2018/03/%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%E6%8A%80%E6%9C%AF%E7%82%B9%E6%A2%B3%E7%90%86/)

# 开源框架和容器
## Servlet
### 什么是 Servlet？
  Servlet 是一些遵从 Java Servlet API 的 Java 类（实现 Servlet 接口的类），这些Java类可以响应请求。

### Servlet 的生命周期
  - 初始化- init()
  - 请求处理 - service()
  - 卸载 Servlet - destroy()

### 转发与重定向的区别

## Spring
### 什么是 Spring，你对 Spring 的理解？
  - Spring是一个轻型容器(light-weight container)，其核心是Bean工厂(Bean Factory)，用以构造我们所需要的M(Model)。
  - 在此基础之上，Spring 提供了AOP（Aspect-Oriented Programming, 面向层面的编程）的实现，用它来提供声明式事务、安全等服务；
  - 对 Bean 工厂的扩展ApplicationContext更加方便我们实现J2EE的应用；
  - DAO/ORM 的实现方便我们进行数据库的开发；
  - Web MVC 和 Spring Web 提供了 Java Web 应用的框架或与其他流行的 Web 框架进行集成。

### BeanFactory 和 FactoryBean？

### BeanFactory 和 ApplicationContext 有什么区别

### Spring Bean 的生命周期，如何被管理的？
  1. Spring 容器 从XML 文件中读取 Bean 的定义，并实例化bean。
  2. Spring 根据 Bean 的定义填充所有的属性。
  3. 如果 Bean 实现了BeanNameAware 接口，Spring 传递 Bean 的ID 到 setBeanName方法。
  4. 如果 Bean 实现了 BeanFactoryAware 接口， Spring 传递 Beanfactory 给 setBeanFactory 方法。
  5. 如果有任何与 Bean 相关联的 BeanPostProcessors，Spring 会在 postProcesserBeforeInitialization()方法内调用它们。
  6. 如果 Bean 实现 IntializingBean 了，调用它的 afterPropertySet 方法，如果 Bean 声明了初始化方法，调用此初始化方法。
  7. 如果有 BeanPostProcessors 和 Bean 关联，这些 Bean 的 postProcessAfterInitialization() 方法将被调用。
  8. 如果 Bean 实现了 DisposableBean，它将调用 destroy()方法。

### Spring IOC 如何实现。可参考[三条路线告诉你如何掌握Spring IoC容器的核心原理](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484890&idx=1&sn=b0d0f5013021b86441e1abd37c6724e7)
### Spring中Bean的作用域，默认的是哪一个？ Singleton

### Spring IOC 的理解，其初始化过程？
  IOC:控制反转也叫依赖注入，IOC利用java反射机制，AOP利用代理模式。所谓控制反转是指，本来被调用者的实例是有调用者来创建的，这样的缺点是耦合性太强，IOC则是统一交给spring来管理创建，将对象交给容器管理，你只需要在spring配置文件总配置相应的bean，以及设置相关的属性，让spring容器来生成类的实例对象以及管理对象。在spring容器启动的时候，spring会把你在配置文件中配置的bean都初始化好，然后在你需要调用的时候，就把它已经初始化好的那些bean分配给你需要调用这些bean的类。

### 说说 Spring AOP
  面向切面编程（AOP）完善spring的依赖注入（DI），面向切面编程在spring中主要表现为两个方面
  1. 面向切面编程提供声明式事务管理
  2. spring支持用户自定义的切面
  AOP：面向切面，是一种编程思想，OOP的延续。将系统中非核心的业务提取出来，进行单独处理。比如事务、日志和安全等。

### Spring AOP 实现原理
  Spring AOP的实现原理是基于动态代理技术，而动态代理技术又分为Java JDK动态代理和CGLIB动态代理。
  + JDK 动态代理
    - 是利用反射机制生成一个实现代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理。
    + 优势：
      - 最小化依赖关系，减少依赖意味着简化开发和维护，JDK 本身的支持，可能比 cglib 更加可靠。
      - 平滑进行 JDK 版本升级，而字节码类库通常需要进行更新以保证在新版 Java 上能够使用。
      - 代码实现简单。
  + CGLIB
    - 是利用asm开源包，对代理对象类的class文件加载进来，通过修改其字节码生成子类来处理。
    - 注意，CGLIB是通过继承的方式做的动态代理，因此如果某个类被标记为final，那么它是无法使用CGLIB做动态代理的，诸如private的方法也是不可以作为切面的。
    - 采取的是创建目标类的子类的方式，因为是子类化，我们可以达到近似使用被调用者本身的效果。
    + 优势：
      - 有的时候调用目标可能不便实现额外接口，从某种角度看，限定调用者实现接口是有些侵入性的实践，类似 cglib 动态代理就没有这种限制。
      - 只操作我们关心的类，而不必为其他相关类增加工作量。
      - 高性能

### Spring 切面可以应用的通知类型有哪些？
  1. before：前置通知，在一个方法执行前被调用。
  2. after: 在方法执行之后调用的通知，无论方法执行是否成功。
  3. after-returning: 仅当方法成功完成后执行的通知。
  4. after-throwing: 在方法抛出异常退出时执行的通知。
  5. around: 在方法执行之前和之后调用的通知。

### 动态代理（CGLib 与 JDK）、优缺点、性能对比、如何选择？

### Spring 事务实现方式、事务的传播机制、默认的事务类别
  + 事务的隔离级别：
    - Read Uncommited （读未提交）
    - Read Commited   （读提交）
    - Read Repeatable （读重复）
    - Serializable    （序列化）
  + 默认事务隔离级别：
    - 大多数数据库默认为 Read Committed
    - MySQL 默认为 Repeatable Committed
  + Spring 支持 7 种事务传播行为：
    - propagation_requierd：     如果当前没有事务，就新建一个事务，如果已存在一个事务中，加入到这个事务中，这是最常见的选择。
    - propagation_supports：     支持当前事务，如果没有当前事务，就以非事务方法执行。
    - propagation_mandatory：    使用当前事务，如果没有当前事务，就抛出异常。
    - propagation_required_new： 新建事务，如果当前存在事务，把当前事务挂起。
    - propagation_not_supported：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。
    - propagation_never：        以非事务方式执行操作，如果当前事务存在则抛出异常。
    - propagation_nested：       如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与propagation_required类似的操作
  - Spring 默认的事务传播行为是 PROPAGATION_REQUIRED，它适合于绝大多数的情况。

### 事务并发访问时可能会出现：脏读、不可重复读和幻读
  - 脏读
    A事务读取了B事务未提交的更改数据。一般数据库事务默认不允许该问题出现。
  - 不可重复读
    指在一个事务内多次读同一数据，在这期间另外一个事务也访问并对该数据进行了修改。这样就造成了第一个事务两次读到的数据不一致，因此称为不可重复读。
  - 幻读
    它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录。请注意，幻读重点是插入或者删除数据导致的（对满足条件的数据行集进行锁定）
### 数据库隔离级别与可能出现的问题
|隔离级别                    |脏读 |不可重复读|幻读|
|Read Uncommited （读未提交）|会   |会        |会|
|Read Commited   （读提交）  |不   |会        |会|
|Read Repeatable （可重复读）|不   |不        |会|
|Serializable    （序列化）  |不   |不        |不|

### MySQL 共享锁和排他锁
  - 共享锁（又称读锁）
    共享锁就是多个事务对于同一数据可以共享一把锁，都能访问到数据，但是只能读不能修改。
  + 排他锁（又称写锁）
    - 如果一个事务获取了一个数据行的排他锁，其他事务就不能再获取该行的其他锁，包括共享锁和排他锁。
    - InnoDB 引擎默认的修改数据语句 update、delete、insert 都会自动给涉及到的数据加上排他锁，select 默认不会加任何锁。
    - 加过排他锁的数据行在其他事务里是不能修改数据的，也不能通过for update 和 lock in share mode 锁的方式查询数据，但可以直接通过 select ...from... 查询数据，因为普通查询没有任何锁机制。

### Spring 事务底层原理
### Spring 事务失效（事务嵌套），JDK 动态代理给 Spring 事务埋下的坑，可参考[JDK动态代理给Spring事务埋下的坑！](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484940&idx=1&sn=0a0a7198e96f57d610d3421b19573002)
### 如何自定义注解实现功能

### Spring MVC 工作原理 & 执行流程？  
  - 工作原理
    1. SpringMvc 把请求交给 DispactherServlet
    2. DispactherServlet 查询一个或者多个 HanderMapping
    3. DispactherServlet 请求 Controller
    4. Controller 进行业务逻辑处理
    5. 找到制定的视图对象
    6. 视图负责渲染返回给客户端
  - 执行流程  
    1. 根据配置文件创建 Spring 的容器
    2. 发送 http 请求到核心控制器
    3. 容器通过映射去寻找业务控制器
    4. 使用适配器找到相应的业务类，在业务类进行封装
    5. 数据放到 Model中 用 Map 传递数据进行页面展示

### Spring MVC 启动流程
### Spring 的单例实现原理
### Spring 框架中用到了哪些设计模式
### Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）
### 有没有用到 Spring Boot，Spring Boot 的认识、原理

1. 你有没有⽤过Spring的 AOP? 是⽤来⼲嘛的? ⼤概会怎么使⽤？

2. 如果⼀个接⼝有2个不同的实现, 那么怎么来Autowire⼀个指定的实现？

3. Spring的声明式事务 @Transaction注解⼀般写在什么位置? 抛出了异常 会⾃动回滚吗？有没有办法控制不触发回滚?

4. 如果想在某个Bean⽣成并装配完毕后执⾏⾃⼰的逻辑，可以什么⽅式实 现？

5. SpringBoot 没有放到web容器⾥为什么能跑HTTP服务？

6. SpringBoot 中如果你想使⽤⾃定义的配置⽂件⽽不仅仅是 application.properties，应该怎么弄？

7. SpringMVC 中 RequestMapping 可以指定GET, POST⽅法么？怎么指定？

8. SpringMVC 如果希望把输出的Object(例如XXResult或者XXResponse)这 种包装为JSON输出, 应该怎么处理?

9. 怎样拦截 SpringMVC 的异常，然后做⾃定义的处理，⽐如打⽇志或者包装 成JSON

10. 1.struts1和struts2的区别

11. .struts2和springMVC的区别

12. spring框架中需要引用哪些jar包，以及这些jar包的用途

13. springMVC的原理

14. springMVC注解的意思

15. spring中beanFactory和ApplicationContext的联系和区别

16. spring注入的几种方式

17. spring如何实现事物管理的

18. springIOC和AOP的原理

19. hibernate中的1级和2级缓存的使用方式以及区别原理

20. spring中循环注入的方式

### MyBatis的原理
### 可参考
  1. [为什么会有Spring](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484822&idx=1&sn=6fbee2a12b31b6102a18d3725671d41b)
  2. [为什么会有Spring AOP](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484827&idx=1&sn=b9d82f3fced6a875f8dfc22e5849b28e)
  3. [Spring历史版本变迁和如今的生态帝国](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484835&idx=1&sn=0210514d6eb53ad623874344f3ce720a)

## Netty
### BIO、NIO和AIO的区别？
### NIO的组成？
### 为什么选择 Netty，Netty的特点？
### 说说业务中，Netty 的使用场景
### Netty的线程模型？
### 什么是 TCP 粘包/拆包，TCP 粘包/拆包的原因及解决方法？
### 了解哪几种序列化协议？
### 如何选择序列化协议？
### Netty的零拷贝实现？
### Netty的高性能表现在哪些方面？
### NIOEventLoopGroup 源码？
### 原生的 NIO 在 JDK 1.7 版本存在 epoll bug
### 说说 Netty 的零拷贝
### Netty 内部执行流程
### Netty 重连实现

## Tomcat
### Tomcat 的基础架构（Server、Service、Connector、Container）
### Tomcat 如何加载 Servlet 的
### Pipeline-Valve 机制
### Tomcat本身的参数你⼀般会怎么调整？
### 可参考：
  1. [四张图带你了解Tomcat系统架构！](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484905&idx=1&sn=6c8acd89476fadbc4cb9ccfda9c9c2e4)

# 分布式
## Nginx
### 请解释什么是C10K问题或者知道什么是C10K问题吗？
### [Nginx简介](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483994&idx=1&sn=b6591f62c7ea6b4adc5a5bf1bf4eac40)
### 正向代理和反向代理.
### Nginx 几种常见的负载均衡策略
### Nginx 服务器上的 Master 和 Worker 进程分别是什么
### 使用“反向代理服务器”的优点是什么?

## 分布式其他
### 什么是 CAP 定理？
  CAP 定理告诉我们，一个分布式系统不可能同时满足一致性（C：Consistency），可用性（A：Availability）和分区容错性（P：Partition tolerance）这三个基本需求，最多只能同时满足其中的两项。
  - **一致性**（Consistency）：指数据在多个副本之间是否能够保持一致的特性。
  - **可用性**（Availability）：指系统提供的服务必须一直处于可用的状态，对于用户的每一个操作请求总是能够在有限的时间内返回结果。
  - **分区容错性**（Partition tolerance）：分区容错性约束了一个分布式系统需要具有瑞安特性：分布式系统在遇到任何网络分区故障的时候，仍然需要能够保证对外提供满足一致性和可用性的服务，除非是整个网络环境都发生了故障。

### 什么是 BASE 理论？
  - BASE 是 Basically Available（基本可用）、Soft state（软状态）和 Eventually consistent（最终一致性）三个短语的简写。
  - BASE 是对 CAP 中一致性和可用性权衡的结果，其来源于对大规模互联网系统分布式实践的总结。
  - BASE 核心思想是即使无法做到强一致性（Strong consistency），但每个应用都可以根据自身的业务特点，采用适当的方式来使系统达到最终一致性（Eventual consistency）。
  - **基本可用**：指分布式系统在出现不可预知故障的时候，允许损失部分可用性（但绝不等价于系统不可用）。
  - **弱状态**：也称软状态，指允许系统中的数据存在中间状态，并认为该中间状态的存在不会影响系统的整体可用性，即允许系统在不同节点的副本之间进行数据同步的过程存在延时。
  - **最终一致性**：强调的是系统中所有的数据副本，在经过一段时间的同步后，最终能够达到一个一直的状态。其本质是需要系统保证最终数据能够达到一致，而不需要实时保证系统数据的强一致性。

### 谈谈业务中使用分布式的场景
### Session 分布式方案
### Session 分布式处理
### 分布式锁的应用场景、分布式锁的产生原因、基本概念
### 分布是锁的常见解决方案
### 分布式事务的常见解决方案
### 集群与负载均衡的算法与实现
### 怎么提升系统的 QPS 和吞吐量
### 如何保证消息的一致性
### CDN 实现原理
### 说说分库与分表设计，可参考[数据库分库分表策略的具体实现方案](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483931&idx=1&sn=6eda41aa81c1243422a603205d2fad22)
### 分库与分表带来的分布式困境与应对之策

## Dubbo
### 什么是 Dubbo ？
  Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的RPC远程服务调用方案，以及SOA服务治理方案。

### 什么是 RPC、如何实现 RPC、RPC 的实现原理，

### Dubbo 中的 SPI 是什么概念
  SPI即Service Provider Interface，服务提供接口.

### Dubbo 的基本原理、执行流程
  + 基本原理：
    1. client 一个线程调用远程接口，生成一个唯一的ID（比如一段随机字符串，UUID等），Dubbo 是使用 AtomicLong 从 0 开始累计数字的。
    2. 将打包的方法调用信息（如调用的接口名称，方法名称，参数值列表等），和处理结果的回调对象 callback，全部封装在一起，组成一个对象object。
    3. 向专门存放调用信息的全局 ConcurrentHashMap 里面 put(ID, object)。
    4. 将 ID 和打包的方法调用信息封装成一对象 connRequest，使用 IoSession.write(connRequest) 异步发送出去。
    5. 当前线程再使用 callback 的 get() 方法试图获取远程返回的结果，在 get() 内部，则使用 synchronized 获取回调对象 callback 的锁，再先检测是否已经获取到结果，如果没有，然后调用 callback 的 wait() 方法，释放 callback 上的锁，让当前线程处于等待状态。
    6. 服务端接收到请求并处理后，将结果（此结果中包含了前面的 ID，即回传）发送给客户端，客户端 socket 连接上专门监听消息的线程收到消息，分析结果，取到 ID，再从前面的 ConcurrentHashMap 里面 get(ID)，从而找到 callback，将方法调用结果设置到 callback 对象里。
    7. 监听线程接着使用 synchronized 获取回调对象 callback 的锁（因为前面调用过wait()，那个线程已释放 callback 的锁了），再 notifyAll()，唤醒前面处于等待状态的线程继续执行（callback的get()方法继续执行就能拿到调用结果了），至此，整个过程结束。

### Dubbo 适用场景：适合于小数据量大并发的服务调用，以及服务消费者机器数远大于服务提供者机器数的情况

### 可参考：
  1. [分布式框架dubbo原理解析](https://my.oschina.net/u/1378920/blog/693374)
  2. [Dubbo入门](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483931&idx=1&sn=6eda41aa81c1243422a603205d2fad22)
  3. [基于HTTP的RPC实现](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483900&idx=1&sn=c5ca198a66a701f81c2ab118fe7a734a)

## Zookeeper
### Zookeeper 典型应用场景
  + **数据发布/订阅** 即所谓的配置中心，是指发布者将数据发布到 Zookeeper 的一个或一系列结点上，供订阅者进行数据订阅，进而达到动态获取数据的目的，实现配置信息的集中式管理和数据的动态更新。
    Zookeeper采用的是推拉相结合的方式：客户端向服务端注册自己需要关注的节点，一旦该节点的数据发生变更，那么服务端就会想相应的客户端发送 Watcher 时间通知，客户端接收到这个消息通知之后，需要主动到服务端获取最新的数据。
  + **负载均衡**
  + **命名服务**
  + **分布式协调/通知**：对于一个在多台机器上部署运行的应用而言，通常需要一个协调者来控制整个系统的运行流程，如分布式事务的处理、机器间的互相协调等。
    通常的做法是不同的客户端都对 Zookeeper 上同一个数据节点进行 Watcher 注册，监听数据节点的变化（包括数据节点本身及其子节点），如果数据节点发生变化，那么所有订阅的客户端都能够接收到相应的 Watcher 通知，并作出相应的处理。
  + **集群管理**：包括集群监控与集群控制两大块
    集群机器存活性监控：监控系统在 /clusterServers 节点上注册一个 Watcher 监听，那么但凡进行动态添加机器的操作，就会在 /clusterServers 节点下创建一个临时节点：/clusterServers/[Hostname]。这样一来，监控系统就能够实时检测到机器的变动情况。
  + **Master选举**
    利用 ZooKeeper 的强一致性，能够很好的保证在分布式高并发情况下节点的创建一定能够保证全局唯一性，即 ZooKeeper 将会保证客户端无法重复创建一个已经存在的数据节点。也就是说，如果同时有多个客户端请求创建同一个节点，那么最终一定只有一个客户端请求能够创建成功。利用这个特性，就能很容易地在分布式环境中进行 Master 选举了。
  + **分布式锁**
    + 排他锁：
      1. 获取锁：所有客户端都会试图通过调用 create() 接口，在 /exclusive_lock 节点下创建临时子节点 /exclusive_lock/lock。ZooKeeper会保证在所有的客户端中，最终只有一个客户端能够创建成功，那么就可以认为该客户端获取了锁。同时，所有没有获取到锁的客户端就需要到 /exclusive_lock 节点上注册一个子节点变更的 Watcher 监听，以便实时监听到 lock 节点的变更情况。
      2. 释放锁：
        - 当前获取锁的客户端机器发生宕机，那么 ZooKeeper 上的这个临时节点（/exclusive_lock/lock）就会被删除
        - 正常执行完业务逻辑后，客户端就会主动将自己创建的临时节点（/exclusive_lock/lock）删除。
  + **分布式队列**

# 微服务
## 微服务
### 前后端分离是如何做的？
### 微服务哪些框架
### Spring Could 的常见组件有哪些？可参考[Spring Cloud概述](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247484125&idx=1&sn=ddba9fba6ae900f5ef71a68f70afebe5)
### 领域驱动有了解吗？什么是领域驱动模型？充血模型、贫血模型
### 什么是 JWT？可参考[前后端分离利器之JWT](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247485183&idx=1&sn=05dac824dbb534710dd99d6c895fbaf5)
### 你怎么理解 RESTful
### 说说如何设计一个良好的 API
### 如何理解 RESTful API 的幂等性
### 如何保证接口的幂等性
### 说说 CAP 定理、BASE 理论
### 怎么考虑数据一致性问题
### 说说最终一致性的实现方案
### 微服务的优缺点，可参考[微服务批判](http://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247485005&idx=1&sn=78a1d286c6a15a81ea5dcf6634a70b54)
### 微服务与 SOA 的区别
### 如何拆分服务、水平分割、垂直分割
### 如何应对微服务的链式调用异常
### 如何快速追踪与定位问题
### 如何保证微服务的安全、认证

## 安全问题
### 如何防范常见的Web攻击、如何方式SQL注入
### 服务端通信安全攻防
### HTTPS 原理剖析、降级攻击、HTTP 与HTTPS 的对比
### OAuth
  - 概念：OAuth 是一个关于授权的开放网络标准。
  + 作用：
    - 不需要将用户名和密码提供给第三方应用而是通过令牌让第三方应用访问资源
    - 每一个令牌授权一个特定的应用在特定的时段内访问特定的资源
  + 授权流程：
    1. 用户打开客户端以后，客户端要求用户给予授权
    2. 用户同意授权
    3. 客户端使用上一步获得的授权，向认证服务器申请令牌
    4. 认证服务器对客户端进行认证以后，确认无误并且发放令牌
    5. 客户端使用令牌向资源服务器申请获取资源
    6. 资源服务器确认令牌无误同意向客户端开放资源      

## 性能优化
### 性能指标有哪些
### 如何发现性能瓶颈
### 性能调优的常见手段
### 说说你在项目中如何进行性能调优


# 其他
## 设计能力
### 说说你在项目中使用过的 UML 图
### 你如何考虑组件化、服务化、系统拆分
### 秒杀场景如何设计
### 有没有处理过线上问题？出现内存泄露，CPU 利用率标高，应用无响应时如何处理的。
### 开发中有没有遇到什么技术问题？如何解决的
### 如果有几十亿的白名单，每天白天需要高并发查询，晚上需要更新一次，如何设计这个功能。
### 新浪微博是如何实现把微博推给订阅者
### Google 是如何在一秒内把搜索结果返回给用户的。
### 12306 网站的订票系统如何实现，如何保证不会票不被超卖。
### 如何实现一个秒杀系统，保证只有几位用户能买到某件商品。
### 可参考：
  1. [秒杀系统的技术挑战、应对策略以及架构设计总结一二！](https://blog.csdn.net/bntx2jsqfehy7/article/details/79407907)
  2. [大型网站应用之海量数据和高并发解决方案总结一二](https://mp.weixin.qq.com/s?__biz=MzI1NDQ3MjQxNA==&mid=2247483917&idx=1&sn=db1b0a2093d3c0d1bb6e32263abfe137)

## 业务工程
### 说说你的开发流程、如何进行自动化部署的
### 你和团队是如何沟通的
### 你如何进行代码评审
### 说说你对技术与业务的理解
### 说说你在项目中遇到感觉最难Bug，是如何解决的
### 介绍一下工作中的一个你认为最有价值的项目，以及在这个过程中的角色、解决的问题、你觉得你们项目还有哪些不足的地方

## 软实力
### 说说你的优缺点、亮点
### 说说你最近在看什么书、什么博客、在研究什么新技术、再看那些开源项目的源代码
### 说说你觉得最有意义的技术书籍
### 工作之余做什么事情、平时是如何学习的，怎样提升自己的能力
### 说说个人发展方向方面的思考
### 说说你认为的服务端开发工程师应该具备哪些能力
### 说说你认为的架构师是什么样的，架构师主要做什么
### 如何看待加班的问题


## 面试技巧  
### 可参考：
  1. [程序员跳槽时，如何高效地准备面试？](http://gitbook.cn/books/5a6985f12a144149588739a5/index.html)
  2. [才震宏：解析程序员跳槽时如何高效地准备面试](http://gitbook.cn/books/5a73206362710202070b47ac/index.html)
  3. [程序员跳槽时，如何正确做好职业规划？](http://gitbook.cn/books/5a9f529e123f227c0649d946/index.html)
  4. [王鹏：解析程序员跳槽时如何正确做好职业规划](http://gitbook.cn/books/5aa9fa860bb9e857450e70ad/index.html)
  5. [程序员跳槽时，如何优雅地谈薪水？](http://gitbook.cn/books/5a951e93ba2cd224ba9480a7/index.html)
  6. [于丽洋：解析程序员跳槽时如何优雅地谈薪水](http://gitbook.cn/books/5aa0bdf7f622f7137a21bf9e/index.html)


# 引用
  1. [你离BAT之间，只差这一套Java面试题](https://mp.weixin.qq.com/s/5nOqRQwq9sykLN2fvRak6w)
