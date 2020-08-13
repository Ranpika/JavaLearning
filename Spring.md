## Spring和SpringBoot区别

`Spring Boot`基本上是`Spring`框架的扩展，它消除了设置`Spring`应用程序所需的`XML配置`，为更快，更高效的开发生态系统铺平了道路。

**Spring Boot中的一些特征：**

1. 创建独立的`Spring`应用。
2. 嵌入式`Tomcat`、`Jetty`、 `Undertow`容器（无需部署war文件）。
3. 提供的`starters` 简化构建配置
4. 尽可能自动配置`spring`应用。
5. 提供生产指标,例如指标、健壮检查和外部化配置
6. 完全没有代码生成和`XML`配置要求



spring mvc 是只是spring 处理web层请求的一个模块。 

因此他们的关系大概就是这样： 

spring mvc < spring <springboot。spring boot 我理解就是把 spring spring mvc spring data jpa 等等的一些常用的常用的基础框架组合起来，提供默认的配置，然后提供可插拔的设计，就是各种 starter ，来方便开发者使用这一系列的技术，套用官方的一句话， spring 家族发展到今天，已经很庞大了，作为一个开发者，如果想要使用 spring 家族一系列的技术，需要一个一个的搞配置，然后还有个版本兼容性问题，其实挺麻烦的，偶尔也会有小坑出现，其实蛮影响开发进度， spring boot 就是来解决这个问题，提供了一个解决方案吧，可以先不关心如何配置，可以快速的启动开发，进行业务逻辑编写，各种需要的技术，加入 starter 就配置好了，直接使用，可以说追求开箱即用的效果吧. 

spring 框架有超多的延伸产品例如 boot security jpa etc... 但它的基础就是 spring 的 ioc 和 aop。 ioc 提供了依赖注入的容器 aop 解决了面向横切面的编程 ，然后在此两者的基础上实现了其他延伸产品的高级功能 。Spring MVC 呢是基于 Servlet 的一个 MVC 框架 ，主要解决 WEB 开发的问题 因为 Spring 的配置太复杂了 各种 XML JavaConfig hin 麻烦 于是懒人改变世界推出了 Spring boot 约定优于配置 简化了 spring 的配置流程. 

Spring 最初利用“工厂模式”（ DI ）和“代理模式”（ AOP ）解耦应用组件。大家觉得挺好用，于是按照这种模式搞了一个 MVC 框架（一些用 Spring 解耦的组件），用开发 web 应用（ SpringMVC ）。然后有发现每次开发都要搞很多依赖，写很多样板代码很麻烦，于是搞了一些懒人整合包（ starter ），这套就是 Spring Boot 。

## IOC和DI

①IOC即控制反转，简单来说就是把对象的控制权委托给spring框架，作用是降低代码的耦合度。

②DI即依赖注入，是IOC的一种具体实现方式。假设一个Car类需要Engine的对象，那么一般需要new一个Engine，利用IOC就是只需要定义一个私有的Engine引用变量，容器会在运行时创建一个Engine的实例对象并将引用自动注入给变量。

## DI的实现方式

①可以注入的数据类型有基本数据类型、String、Bean以及集合等复杂数据类型。

②有三种注入方式，

- 第一种是通过构造器注入，通过constructor-arg标签实现，缺点是即使不需要该属性也必须注入；
- 第二种是通过Set方法注入，通过property标签实现，优点是创建对象时没有明确限制，缺点是某个成员变量必须有值，在获取对象时set方法可能还没有执行；
- 第三种是通过注解注入，
  - 利用@Autowired自动按类型注入，如果有多个匹配则按照指定bean的id查找，查找不到会报错；
  - @Qualifier在自动按照类型注入的基础之上，再按照 Bean 的 id 注入，给成员变量注入时必须搭配@Autowired，给方法注入时可单独使用；
  - @Resource直接按照 Bean 的 id 注入；
  - @Value用于注入基本数据类型和String。
  - 集合类型的注入只能通过xml实现

## 为什么用注解

1、如果所有的内容都配置在.xml文件中，那么.xml文件将会十分庞大；如果按需求分开.xml文件，那么.xml文件又会非常多。总之这将导致配置文件的可读性与可维护性变得很低。 

2、在开发中在.java文件和.xml文件之间不断切换，是一件麻烦的事，同时这种思维上的不连贯也会降低开发的效率。 

为了解决这两个问题，Spring引入了注解，通过"@XXX"的方式，让注解与Java Bean紧密结合，既大大减少了配置文件的体积，又增加了Java Bean的可读性与内聚性。

## BeanFactory、FactoryBean、ApplicationContext的区别（阿里）

①BeanFactory是一个Factory顶层接口，是用来管理bean的IOC容器或对象工厂，较为古老，不支持spring的一些插件。BeanFactory使用了延迟加载，适合多例模式。

- 在Spring中，**所有的Bean都是由BeanFactory(也就是IOC容器)来进行管理的**

②FactoryBean是一个Bean接口，是一个可以生产或者装饰对象的工厂Bean，可以通过实现该接口自定义的实例化Bean的逻辑。

- 对FactoryBean而言，**这个Bean不是简单的Bean，而是一个能生产或者修饰对象生成的工厂Bean,它的实现与设计模式中的工厂模式和修饰器模式类似** 

③ApplicationConext是BeanFactory的子接口，扩展了其功能，ApplicationContext是立即加载，适合单例模式。一般推荐使用ApplicationContext。



## 代理方式：静态代理、动态代理 区别

Proxy代理模式是一种结构型设计模式，主要解决的问题是：在直接访问对象时带来的问题

代理是一种常用的设计模式，其目的就是**为其他对象提供一个代理以控制对某个对象的访问**。代理类负责为委托类预处理消息，过滤消息并转发消息，以及进行消息被委托类执行后的后续处理。

动态代理：

基于JDK技术 动态代理类技术核心 继承Proxy类，实现一个 InvocationHandler 接口

动态代理好处：

在接口方法数量比较多的时候，我们可以进行灵活处理，而不需要像静态代理那样每一个方法进行中转。而且动态代理的应用使我们的类职责更加单一，复用性更强。

https://blog.csdn.net/fangqun663775/article/details/78960545

https://www.cnblogs.com/gonjan-blog/p/6685611.html

https://cloud.tencent.com/developer/article/1461796

## 单例模式

懒汉式、饿汉式

Spring如何实现单例singleton：单例注册表

**注册登记式单例**：每使用一次，都往一个固定的容器中去注册并且将使用过的对象进行缓存，下次取对象的时候直接从缓存中取值，以保证每次获取的都是同一个对象。

https://blog.csdn.net/w1014074794/article/details/88403568

①单例模式是**保证系统实例唯一性**的重要手段。单例模式首先通过**将类的实例化方法私有化**来防止程序通过其他方式创建该类的实例，然后通过**提供一个全局唯一获取该类实例的方法**帮助用户获取类的实例，用户只需也只能通过调用该方法获取类的实例。

②单例模式的设计**保证了一个类在整个系统中同一时刻只有一个实例存在**，主要被用于一个全局类的对象在多个地方被使用并且对象的状态是全局变化的场景下。同时单例模式为系统资源的优化提供了很好的思路，频繁创建或销毁对象都会增加系统的资源消耗，而单例模式**保障了整个系统只有一个对象能被使用，很好地节约了资源。**

饿汉式：线程安全，没有加锁执行效率高，但类加载时就创建了实例，可能浪费内存资源。

懒汉式：线程不安全，在使用时才创建实例，可以通过双重锁机制保证线程安全，或使用静态内部类优化效率。

反射和序列化会破坏单例模式，在序列化添加readResolve可以解决该问题，但实际上还是实例化了两次只是新创建的对象没有被返回，如果创建对象的频率很快，内存的开销也会更大。

还可以使用注册式单例模式，可以使用枚举式单例模式，反编译后可以发现在静态代码块中实例化，属于饿汉式，同时不会被反射破坏，当修饰符是枚举类型时会抛出异常。也可以使用容器式单例模式，使用HashMap，适用于实例非常多的情况，方便管理但是线程不安全，可以使用ConcurrentHashMap。



## Bean的作用域和生命周期

![img](https://img-blog.csdn.net/20160417164310654?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

五种作用域中，request、session和global session三种作用域仅在基于web的应用中使用（不必关心你所采用的是什么web应用框架），只能用在基于web的Spring ApplicationContext环境。

![这里写图片描述](https://img-blog.csdn.net/20180426085835757?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dfbGludXg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![img](https://img-blog.csdn.net/20180802223029954?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTIzODUxOTA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

Spring对bean进行实例化，默认bean是单例；

Spring对bean进行依赖注入；

如果bean实现了BeanNameAware接口，spring将bean的id传给setBeanName()方法；

如果bean实现了BeanFactoryAware接口，spring将调用setBeanFactory方法，将BeanFactory实例传进来；

如果bean实现了ApplicationContextAware接口，它的setApplicationContext()方法将被调用，将应用上下文的引用传入到bean中；

如果bean实现了BeanPostProcessor接口，它的postProcessBeforeInitialization方法将被调用；

如果bean实现了InitializingBean接口，spring将调用它的afterPropertiesSet接口方法，类似的如果bean使用了init-method属性声明了初始化方法，该方法也会被调用；

如果bean实现了BeanPostProcessor接口，它的postProcessAfterInitialization接口方法将被调用；

此时bean已经准备就绪，可以被应用程序使用了，他们将一直驻留在应用上下文中，直到该应用上下文被销毁；

若bean实现了DisposableBean接口，spring将调用它的distroy()接口方法。同样的，如果bean使用了destroy-method属性声明了销毁方法，则该方法被调用；
————————————————
版权声明：本文为CSDN博主「fuzhongmin05」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/fuzhongmin05/article/details/73389779

```
①Spring对bean进行实例化。

②Spring将值和bean的引用注入到其对应的属性中。

③调用BeanNameAware的setBeanName方法。

④调用BeanFactoryAware的setBeanFactory方法。

⑤调用AppicationContextAware的setApplicationContext方法。

⑥调用BeanPostProcessor的post-ProcessBeforeInitialization方法。

⑦调用InitializingBean的after-PropertiesSet方法。如果bean使用init-method声明了自定义初始化方法，该方法也会被调用。

⑧调用BeanPostProcessor的post-ProcessAfterInitialization方法。

⑨使用bean。

⑩调用DisposableBean的destroy方法，如果bean使用destroy-method声明了自定义销毁方法，该方法也会被调用。
```



## 使用XML配置创建Bean对象的方式

①通过默认无参构造器。使用bean标签，只使用id和class属性，如果没有无参构造器会报错。

②使用静态工厂，通过bean标签中的class指明静态工厂，factory-method指明静态工厂方法。

③使用实例工厂，通过bean标签中的factory-bean指明实例工厂，factory-method指明实例工厂方法。

## Aop的基本思想，原理，相关的注解（阿里、招行）

### 思想和原理

Aop即面向切面编程，简单地说就是将代码中重复的部分抽取出来，在需要执行的时候**使用动态代理的技术，在不修改源码的基础上对方法进行增强**。优点是可以**减少代码的冗余，提高开发效率，维护方便。**

- Spring会根据类是否实现了接口来判断动态代理的方式，如果**实现了接口会使用JDK的动态代理，核心是InvocationHandler接口和Proxy类，如果没有实现接口会使用cglib的动态代理，cglib是在运行时动态生成某个类的子类**，如果某一个类被标记为final，是不能使用cglib动态代理的。

### cglib和jdk动态代理的区别

①jdk动态代理是利用**反射机制**生成一个实现代理接口的**匿名类**，在调用具体方法前调用**InvokeHandler**来处理。

- JDK的动态代理主要通过重组字节码实现，首先获得被代理对象的引用和所有接口，生成新的类必须实现被代理类的所有接口，动态生成Java代码后编译新生成的.class文件并重新加载到JVM运行。JDK代理直接写Class字节码

②cglib的原理是对指定的目标类**生成一个子类**，**并覆盖其中方法实现增强**，但因为采用的是**继承**，所以不能对final修饰的类和方法进行代理。

- CGLib是采用ASM框架写字节码，**生成代理类的效率低**。但是CGLib**调用方法的效率高**，因为JDK使用反射来调用方法，CGLib使用FastClass机制为代理类和被代理类各生成一个类，这个类会为代理类或被代理类的方法生成一个index，这个index可以作为参数直接定位要调用的方法。

### 相关注解

①@Before前置通知，@AfterThrowing异常通知，@AfterReturning后置通知，@After最终通知，@Around环绕通知。

②最终通知会在后置通知之前执行，为解决此问题一般使用环绕通知。

### 专业术语

①Joinpoint(连接点):指那些被拦截到的点，在 spring 中这些点指的是方法，因为 spring 只支持方法类型的连接点。例如业务层实现类中的方法都是连接点。

②Pointcut(切入点):指我们要对哪些 Joinpoint 进行拦截的定义。例如业务层实现类中被增强的方法都是切入点，切入点一定是连接点，但连接点不一定是切入点。

③Advice(通知/增强):指拦截到 Joinpoint 之后所要做的事情。

④Introduction(引介):引介是一种特殊的通知，在不修改类代码的前提下可以在运行期为类动态地添加一些方法或 Field。

⑤Weaving(织入):是指把增强应用到目标对象来创建新的代理对象的过程。spring 采用动态代理织入，而 AspectJ 采用编译期织入和类装载期织入。

⑥Proxy（代理）:一个类被 AOP 织入增强后，就产生一个结果代理类。

⑦Target(目标):代理的目标对象。

⑧Aspect(切面):是切入点和通知（引介）的结合。



## 网上整理常见问题

作者：冠状病毒biss
链接：https://www.nowcoder.com/discuss/447742?type=0&order=7&pos=153&page=4&source_id=discuss_center_0&channel=1013
来源：牛客网



### Spring IoC 11

#### Q1：IoC 是什么？

IoC 即控制反转，简单来说就是把原来代码里需要实现的对象创建、依赖反转给容器来帮忙实现，需要创建一个容器并且需要一种描述让容器知道要创建的对象间的关系，在 Spring 中管理对象及其依赖关系是通过 Spring 的 IoC 容器实现的。

IoC 的实现方式有依赖注入和依赖查找，由于依赖查找使用的很少，因此 IoC 也叫做依赖注入。依赖注入指对象被动地接受依赖类而不用自己主动去找，对象不是从容器中查找它依赖的类，而是在容器实例化对象时主动将它依赖的类注入给它。假设一个 Car 类需要一个 Engine 的对象，那么一般需要需要手动 new 一个 Engine，利用 IoC 就只需要定义一个私有的 Engine 类型的成员变量，容器会在运行时自动创建一个 Engine 的实例对象并将引用自动注入给成员变量。

------

#### Q2：IoC 容器初始化过程？

**基于 XML 的容器初始化**

当创建一个 ClassPathXmlApplicationContext 时，构造方法做了两件事：① 调用父容器的构造方法为容器设置好 Bean 资源加载器。② 调用父类的 `setConfigLocations` 方法设置 Bean 配置信息的定位路径。

ClassPathXmlApplicationContext 通过调用父类 AbstractApplicationContext 的 `refresh` 方法启动整个 IoC 容器对 Bean 定义的载入过程，`refresh` 是一个模板方法，规定了 IoC 容器的启动流程。在创建 IoC 容器前如果已有容器存在，需要把已有的容器销毁，保证在 `refresh` 方法后使用的是新创建的 IoC 容器。

容器创建后通过 `loadBeanDefinitions` 方法加载 Bean 配置资源，该方法做两件事：① 调用资源加载器的方法获取要加载的资源。② 真正执行加载功能，由子类 XmlBeanDefinitionReader 实现。加载资源时首先解析配置文件路径，读取配置文件的内容，然后通过 XML 解析器将 Bean 配置信息转换成文档对象，之后按照 Spring Bean 的定义规则对文档对象进行解析。

Spring IoC 容器中注册解析的 Bean 信息存放在一个 HashMap 集合中，key 是字符串，值是 BeanDefinition，注册过程中需要使用 synchronized 保证线程安全。当配置信息中配置的 Bean 被解析且被注册到 IoC 容器中后，初始化就算真正完成了，Bean 定义信息已经可以使用且可被检索。Spring IoC 容器的作用就是对这些注册的 Bean 定义信息进行处理和维护，注册的 Bean 定义信息是控制反转和依赖注入的基础。

**基于注解的容器初始化**

分为两种：① 直接将注解 Bean 注册到容器中，可以在初始化容器时注册，也可以在容器创建之后手动注册，然后刷新容器使其对注册的注解 Bean 进行处理。② 通过扫描指定的包及其子包的所有类处理，在初始化注解容器时指定要自动扫描的路径。

------

#### Q3：依赖注入的实现方法有哪些？

**构造方法注入：** IoC Service Provider 会检查被注入对象的构造方法，取得它所需要的依赖对象列表，进而为其注入相应的对象。这种方法的优点是在对象构造完成后就处于就绪状态，可以马上使用。缺点是当依赖对象较多时，构造方法的参数列表会比较长，构造方法无法被继承，无法设置默认值。对于非必需的依赖处理可能需要引入多个构造方法，参数数量的变动可能会造成维护的困难。

**setter 方法注入：** 当前对象只需要为其依赖对象对应的属性添加 setter 方法，就可以通过 setter 方法将依赖对象注入到被依赖对象中。setter 方法注入在描述性上要比构造方法注入强，并且可以被继承，允许设置默认值。缺点是无法在对象构造完成后马上进入就绪状态。

**接口注入：** 必须实现某个接口，接口提供方法来为其注入依赖对象。使用少，因为它强制要求被注入对象实现不必要接口，侵入性强。

------

#### Q4：依赖注入的相关注解？

`@Autowired`：自动按类型注入，如果有多个匹配则按照指定 Bean 的 id 查找，查找不到会报错。

`@Qualifier`：在自动按照类型注入的基础上再按照 Bean 的 id 注入，给变量注入时必须搭配 `@Autowired`，给方法注入时可单独使用。

`@Resource` ：直接按照 Bean 的 id 注入，只能注入 Bean 类型。

`@Value` ：用于注入基本数据类型和 String 类型。

------

#### Q5：依赖注入的过程？

`getBean` 方法获取 Bean 实例，该方***调用 `doGetBean` ，`doGetBean` 真正实现从 IoC 容器获取 Bean 的功能，也是触发依赖注入的地方。

具体创建 Bean 对象的过程由 ObjectFactory 的 `createBean` 完成，该方法主要通过 `createBeanInstance` 方法生成 Bean 包含的 Java 对象实例和 `populateBean` 方法对 Bean 属性的依赖注入进行处理。

在 `populateBean`方法中，注入过程主要分为两种情况：① 属性值类型不需要强制转换时，不需要解析属性值，直接进行依赖注入。② 属性值类型需要强制转换时，首先解析属性值，然后对解析后的属性值进行依赖注入。依赖注入的过程就是将 Bean 对象实例设置到它所依赖的 Bean 对象属性上，真正的依赖注入是通过 `setPropertyValues` 方法实现的，该方法使用了委派模式。

BeanWrapperImpl 类负责对完成初始化的 Bean 对象进行依赖注入，对于非集合类型属性，使用 JDK 反射，通过属性的 setter 方法为属性设置注入后的值。对于集合类型的属性，将属性值解析为目标类型的集合后直接赋值给属性。

当容器对 Bean 的定位、载入、解析和依赖注入全部完成后就不再需要手动创建对象，IoC 容器会自动为我们创建对象并且注入依赖。

------

#### Q6：Bean 的生命周期？

在 IoC 容器的初始化过程中会对 Bean 定义完成资源定位，加载读取配置并解析，最后将解析的 Bean 信息放在一个 HashMap 集合中。当 IoC 容器初始化完成后，会进行对 Bean 实例的创建和依赖注入过程，注入对象依赖的各种属性值，在初始化时可以指定自定义的初始化方法。经过这一系列初始化操作后 Bean 达到可用状态，接下来就可以使用 Bean 了，当使用完成后会调用 destroy 方法进行销毁，此时也可以指定自定义的销毁方法，最终 Bean 被销毁且从容器中移除。

XML 方式通过配置 bean 标签中的 init-Method 和 destory-Method 指定自定义初始化和销毁方法。 

注解方式通过 `@PreConstruct` 和 `@PostConstruct` 注解指定自定义初始化和销毁方法。

------

#### Q7：Bean 的作用范围？

通过 scope 属性指定 bean 的作用范围，包括：

① singleton：单例模式，是默认作用域，不管收到多少 Bean 请求每个容器中只有一个唯一的 Bean 实例。

② prototype：原型模式，和 singleton 相反，每次 Bean 请求都会创建一个新的实例。

③ request：每次 HTTP 请求都会创建一个新的 Bean 并把它放到 request 域中，在请求完成后 Bean 会失效并被垃圾收集器回收。

④ session：和 request 类似，确保每个 session 中有一个 Bean 实例，session 过期后 bean 会随之失效。

⑤ global session：当应用部署在 Portlet 容器时，如果想让所有 Portlet 共用全局存储变量，那么该变量需要存储在 global session 中。

------

#### Q8：如何通过 XML 方式创建 Bean？

默认无参构造方法，只需要指明 bean 标签中的 id 和 class 属性，如果没有无参构造方***报错。

静态工厂方法，通过 bean 标签中的 class 属性指明静态工厂，factory-method 属性指明静态工厂方法。

实例工厂方法，通过 bean 标签中的 factory-bean 属性指明实例工厂，factory-method 属性指明实例工厂方法。

------

#### Q9：如何通过注解创建 Bean？

`@Component` 把当前类对象存入 Spring 容器中，相当于在 xml 中配置一个 bean 标签。value 属性指定 bean 的 id，默认使用当前类的首字母小写的类名。

`@Controller`，`@Service`，`@Repository` 三个注解都是 `@Component` 的衍生注解，作用及属性都是一模一样的。只是提供了更加明确语义，`@Controller` 用于表现层，`@Service`用于业务层，`@Repository`用于持久层。如果注解中有且只有一个 value 属性要赋值时可以省略 value。

如果想将第三方的类变成组件又没有源代码，也就没办法使用 `@Component` 进行自动配置，这种时候就要使用 `@Bean` 注解。被 `@Bean` 注解的方法返回值是一个对象，将会实例化，配置和初始化一个新对象并返回，这个对象由 Spring 的 IoC 容器管理。name 属性用于给当前 `@Bean` 注解方法创建的对象指定一个名称，即 bean 的 id。当使用注解配置方法时，如果方法有参数，Spring 会去容器查找是否有可用 bean对象，查找方式和 `@Autowired` 一样。

------

#### Q10：如何通过注解配置文件？

`@Configuration` 用于指定当前类是一个 spring 配置类，当创建容器时会从该类上加载注解，value 属性用于指定配置类的字节码。

`@ComponentScan` 用于指定 Spring 在初始化容器时要扫描的包。basePackages 属性用于指定要扫描的包。

`@PropertySource` 用于加载 `.properties` 文件中的配置。value 属性用于指定文件位置，如果是在类路径下需要加上 classpath。

`@Import` 用于导入其他配置类，在引入其他配置类时可以不用再写 `@Configuration` 注解。有 `@Import` 的是父配置类，引入的是子配置类。value 属性用于指定其他配置类的字节码。

------

#### Q11：BeanFactory、FactoryBean 和 ApplicationContext 的区别？

BeanFactory 是一个 Bean 工厂，使用简单工厂模式，是 Spring IoC 容器顶级接口，可以理解为含有 Bean 集合的工厂类，作用是管理 Bean，包括实例化、定位、配置对象及建立这些对象间的依赖。BeanFactory 实例化后并不会自动实例化 Bean，只有当 Bean 被使用时才实例化与装配依赖关系，属于延迟加载，适合多例模式。

FactoryBean 是一个工厂 Bean，使用了工厂方法模式，作用是生产其他 Bean 实例，可以通过实现该接口，提供一个工厂方法来自定义实例化 Bean 的逻辑。FactoryBean 接口由 BeanFactory 中配置的对象实现，这些对象本身就是用于创建对象的工厂，如果一个 Bean 实现了这个接口，那么它就是创建对象的工厂 Bean，而不是 Bean 实例本身。

ApplicationConext 是 BeanFactory 的子接口，扩展了 BeanFactory 的功能，提供了支持国际化的文本消息，统一的资源文件读取方式，事件传播以及应用层的特别配置等。容器会在初始化时对配置的 Bean 进行预实例化，Bean 的依赖注入在容器初始化时就已经完成，属于立即加载，适合单例模式，一般推荐使用。

------

### Spring AOP 4

#### Q1：AOP 是什么？

AOP 即面向切面编程，简单地说就是将代码中重复的部分抽取出来，在需要执行的时候使用动态代理技术，在不修改源码的基础上对方法进行增强。

Spring 根据类是否实现接口来判断动态代理方式，如果实现接口会使用 JDK 的动态代理，核心是 InvocationHandler 接口和 Proxy 类，如果没有实现接口会使用 CGLib 动态代理，CGLib 是在运行时动态生成某个类的子类，如果某个类被标记为 final，不能使用 CGLib 。

JDK 动态代理主要通过重组字节码实现，首先获得被代理对象的引用和所有接口，生成新的类必须实现被代理类的所有接口，动态生成Java 代码后编译新生成的 `.class` 文件并重新加载到 JVM 运行。JDK 代理直接写 Class 字节码，CGLib 是采用 ASM 框架写字节码，生成代理类的效率低。但是 CGLib 调用方法的效率高，因为 JDK 使用反射调用方法，CGLib 使用 FastClass 机制为代理类和被代理类各生成一个类，这个类会为代理类或被代理类的方法生成一个 index，这个 index 可以作为参数直接定位要调用的方法。

常用场景包括权限认证、自动缓存、错误处理、日志、调试和事务等。

------

#### Q2：AOP 的相关注解有哪些？

`@Aspect`：声明被注解的类是一个切面 Bean。

`@Before`：前置通知，指在某个连接点之前执行的通知。

`@After`：后置通知，指某个连接点退出时执行的通知（不论正常返回还是异常退出）。

`@AfterReturning`：返回后通知，指某连接点正常完成之后执行的通知，返回值使用returning属性接收。

`@AfterThrowing`：异常通知，指方法抛出异常导致退出时执行的通知，和`@AfterReturning`只会有一个执行，异常使用throwing属性接收。

------

#### Q3：AOP 的相关术语有什么？

`Aspect`：切面，一个关注点的模块化，这个关注点可能会横切多个对象。

`Joinpoint`：连接点，程序执行过程中的某一行为，即业务层中的所有方法。。

`Advice`：通知，指切面对于某个连接点所产生的动作，包括前置通知、后置通知、返回后通知、异常通知和环绕通知。

`Pointcut`：切入点，指被拦截的连接点，切入点一定是连接点，但连接点不一定是切入点。

`Proxy`：代理，Spring AOP 中有 JDK 动态代理和 CGLib 代理，目标对象实现了接口时采用 JDK 动态代理，反之采用 CGLib 代理。

`Target`：代理的目标对象，指一个或多个切面所通知的对象。

`Weaving` ：织入，指把增强应用到目标对象来创建代理对象的过程。

------

#### Q4：AOP 的过程？

Spring AOP 由 BeanPostProcessor 后置处理器开始，这个后置处理器是一个***，可以监听容器触发的 Bean 生命周期事件，向容器注册后置处理器以后，容器中管理的 Bean 就具备了接收 IoC 容器回调事件的能力。BeanPostProcessor 的调用发生在 Spring IoC 容器完成 Bean 实例对象的创建和属性的依赖注入后，为 Bean 对象添加后置处理器的入口是 `initializeBean` 方法。

Spring 中 JDK 动态代理通过 JdkDynamicAopProxy 调用 Proxy 的 `newInstance` 方法来生成代理类，JdkDynamicAopProxy 也实现了 InvocationHandler 接口，`invoke` 方法的具体逻辑是先获取应用到此方法上的拦截器链，如果有拦截器则创建 MethodInvocation 并调用其 `proceed` 方法，否则直接反射调用目标方法。因此 Spring AOP 对目标对象的增强是通过拦截器实现的。

------

### Spring MVC 3

#### Q1：Spring MVC 的处理流程？

Web 容器启动时会通知 Spring 初始化容器，加载 Bean 的定义信息并初始化所有单例 Bean，然后遍历容器中的 Bean，获取每一个 Controller 中的所有方法访问的 URL，将 URL 和对应的 Controller 保存到一个 Map 集合中。

所有的请求会转发给 DispatcherServlet 前端处理器处理，DispatcherServlet 会请求 HandlerMapping 找出容器中被 `@Controler` 注解修饰的 Bean 以及被 `@RequestMapping` 修饰的方法和类，生成 Handler 和 HandlerInterceptor 并以一个 HandlerExcutionChain 处理器执行链的形式返回。

之后 DispatcherServlet 使用 Handler 找到对应的 HandlerApapter，通过 HandlerApapter 调用 Handler 的方法，将请求参数绑定到方法的形参上，执行方法处理请求并得到 ModelAndView。

最后 DispatcherServlet 根据使用 ViewResolver 试图解析器对得到的 ModelAndView 逻辑视图进行解析得到 View 物理视图，然后对视图渲染，将数据填充到视图中并返回给客户端。

------

#### Q2：Spring MVC 有哪些组件？

`DispatcherServlet`：SpringMVC 中的前端控制器，是整个流程控制的核心，负责接收请求并转发给对应的处理组件。

`Handler`：处理器，完成具体业务逻辑，相当于 Servlet 或 Action。

`HandlerMapping`：完成 URL 到 Controller 映射，DispatcherServlet 通过 HandlerMapping 将不同请求映射到不同 Handler。

`HandlerInterceptor`：处理器拦截器，是一个接口，如果需要完成一些拦截处理，可以实现该接口。

`HandlerExecutionChain`：处理器执行链，包括两部分内容：Handler 和 HandlerInterceptor。

`HandlerAdapter`：处理器适配器，Handler执行业务方法前需要进行一系列操作，包括表单数据验证、数据类型转换、将表单数据封装到JavaBean等，这些操作都由 HandlerAdapter 完成。DispatcherServlet 通过 HandlerAdapter 来执行不同的 Handler。

`ModelAndView`：装载模型数据和视图信息，作为 Handler 处理结果返回给 DispatcherServlet。

`ViewResolver`：视图解析器，DispatcherServlet 通过它将逻辑视图解析为物理视图，最终将渲染的结果响应给客户端。

------

#### Q3：Spring MVC 的相关注解？

`@Controller`：在类定义处添加，将类交给IoC容器管理。

`@RequtestMapping`：将URL请求和业务方法映射起来，在类和方法定义上都可以添加该注解。`value` 属性指定URL请求的实际地址，是默认值。`method` 属性限制请求的方法类型，包括GET、POST、PUT、DELETE等。如果没有使用指定的请求方法请求URL，会报405 Method Not Allowed 错误。`params` 属性限制必须提供的参数，如果没有会报错。

`@RequestParam`：如果 Controller 方法的形参和 URL 参数名一致可以不添加注解，如果不一致可以使用该注解绑定。`value` 属性表示HTTP请求中的参数名。`required` 属性设置参数是否必要，默认false。`defaultValue` 属性指定没有给参数赋值时的默认值。

`@PathVariable`：Spring MVC 支持 RESTful 风格 URL，通过 `@PathVariable` 完成请求参数与形参的绑定。

------

### Spring Data JPA 4

#### Q1：ORM 是什么？

ORM 即 Object-Relational Mapping ，表示对象关系映射，映射的不只是对象的值还有对象之间的关系，通过 ORM 就可以把对象映射到关系型数据库中。操作实体类就相当于操作数据库表，可以不再重点关注 SQL 语句。

------

#### Q2：JPA 如何使用？

只需要持久层接口继承 JpaRepository 即可，泛型参数列表中第一个参数是实体类类型，第二个参数是主键类型。

运行时通过 `JdkDynamicAopProxy` 的 `invoke` 方法创建了一个动态代理对象 `SimpleJpaRepository`，`SimpleJpaRepository` 中封装了 JPA 的操作，通过 `hibernate`（封装了JDBC）完成数据库操作。

------

#### Q3：JPA 实体类相关注解有哪些？

`@Entity`：表明当前类是一个实体类。

`@Table` ：关联实体类和数据库表。

`@Column` ：关联实体类属性和数据库表中字段。

`@Id` ：声明当前属性为数据库表主键对应的属性。

`@GeneratedValue`： 配置主键生成策略。

`@OneToMany` ：配置一对多关系，mappedBy 属性值为主表实体类在从表实体类中对应的属性名。

`@ManyToOne` ：配置多对一关系，targetEntity 属性值为主表对应实体类的字节码。

`@JoinColumn`：配置外键关系，name 属性值为外键名称，referencedColumnName 属性值为主表主键名称。

------

#### Q4：对象导航查询是什么？

通过 get 方法查询一个对象的同时，通过此对象可以查询它的关联对象。

对象导航查询一到多默认使用延迟加载的形式， 关联对象是集合，因此使用立即加载可能浪费资源。

对象导航查询多到一默认使用立即加载的形式， 关联对象是一个对象，因此使用立即加载。

如果要改变加载方式，在实体类注解配置加上 fetch 属性即可，LAZY 表示延迟加载，EAGER 表示立即加载。

------

### Mybatis 5

#### Q1：Mybatis 的优缺点？

**优点**

相比 JDBC 减少了大量代码量，减少冗余代码。

使用灵活，SQL 语句写在 XML 里，从程序代码中彻底分离，降低了耦合度，便于管理。

提供 XML 标签，支持编写动态 SQL 语句。

提供映射标签，支持对象与数据库的 ORM 字段映射关系。

**缺点**

SQL 语句编写工作量较大，尤其是字段和关联表多时。

SQL 语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。

------

#### Q2：Mybatis 的 XML 文件有哪些标签属性？

`select`、`insert`、`update`、`delete` 标签分别对应查询、添加、更新、删除操作。

`parameterType` 属性表示参数的数据类型，包括基本数据类型和对应的包装类型、String 和 Java Bean 类型，当有多个参数时可以使用 `#{argn}` 的形式表示第 n 个参数。除了基本数据类型都要以全限定类名的形式指定参数类型。

`resultType` 表示返回的结果类型，包括基本数据类型和对应的包装类型、String 和 Java Bean 类型。还可以使用把返回结果封装为复杂类型的 `resultMap` 。

------

#### Q3：Mybatis 的一级缓存是什么？

一级缓存是 SqlSession 级别，默认开启且不能关闭。

操作数据库时需要创建 SqlSession 对象，对象中有一个 HashMap 存储缓存数据，不同 SqlSession 之间缓存数据区域互不影响。

一级缓存的作用域是 SqlSession 范围的，在同一个 SqlSession 中执行两次相同的 SQL 语句时，第一次执行完毕会将结果保存在缓存中，第二次查询直接从缓存中获取。

如果 SqlSession 执行了 DML 操作（insert、update、delete），Mybatis 必须将缓存清空保证数据有效性。 

------

#### Q4：Mybatis 的二级缓存是什么？

二级缓存是Mapper 级别，默认关闭。

使用二级缓存时多个 SqlSession 使用同一个 Mapper 的 SQL 语句操作数据库，得到的数据会存在二级缓存区，同样使用 HashMap 进行数据存储，相比于一级缓存，二级缓存范围更大，多个 SqlSession 可以共用二级缓存，作用域是 Mapper 的同一个 namespace，不同 SqlSession 两次执行相同的 namespace 下的 SQL 语句，参数也相等，则第一次执行成功后会将数据保存在二级缓存中，第二次可直接从二级缓存中取出数据。

要使用二级缓存，需要在全局配置文件中配置 `<setting name="cacheEnabled" value="true"/>` ，再在对应的映射文件中配置一个 `<cache/>` 标签。

------

#### Q5：Mybatis `#{}` 和 `${}` 的区别？

使用 `${}` 相当于使用字符串拼接，存在 SQL 注入的风险。

使用 `#{}` 相当于使用占位符，可以防止 SQL 注入，不支持使用占位符的地方就只能使用 `${}` ，典型情况就是动态参数。