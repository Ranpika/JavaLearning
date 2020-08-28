## 三大特性：继承、封装、多态

**封装**隐藏了类的内部实现机制，可以在不影响使用的情况下改变类的内部结构，同时也保护了数据。对外界而言它的内部细节是隐藏的，暴露给外界的只是它的访问方法。

**继承**是为了重用父类代码。两个类若存在IS-A的关系就可以使用继承，同时继承也为实现多态做了铺垫。

**多态**：

多态就是指程序中定义的**引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定**，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以**让引用变量绑定到各种不同的类实现上**，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。

子类Child继承父类Father，我们可以编写一个指向子类的父类类型引用，该引用既可以处理父类Father对象，也可以处理子类Child对象，当相同的消息发送给子类或者父类对象时，该对象就会根据自己所属的引用而执行不同的行为，这就是多态。即多态性就是**相同的消息使得不同的类做出不同的响应**。

 1  Java实现多态有三个**必要条件**：**继承、重写、向上转型。**

- 继承：在多态中必须存在有继承关系的子类和父类。

- 重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。

- 向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才能够具备技能调用父类的方法和子类的方法。

​     只有满足了上述三个条件，我们才能够在同一个继承结构中使用统一的逻辑实现代码处理不同的对象，从而达到执行不同的行为。

   对于Java而言，它多态的实现机制遵循一个原则：当超类对象引用变量（前面的）引用子类对象（后面的）时，被引用对象的类型而不是引用变量的类型决定了调用谁的成员方法，但是这个被调用的方法必须是在超类中定义过的，也就是说被子类覆盖的方法。

2 在Java中有两种形式可以**实现多态：继承和接口**。

- 基于继承的实现机制主要表现在父类和继承该父类的一个或多个子类对某些方法的**重写**，**多个子类对同一方法的重写可以表现出不同的行为**。
  - 对于引用子类的父类类型，在处理该引用时，它适用于继承该父类的所有子类，子类对象的不同，对方法的实现也就不同，执行相同动作产生的行为也就不同。
  - 如果父类是**抽象类**，那么子类必须要实现父类中所有的**抽象方法**，这样该父类所有的子类一定存在统一的**对外接口**，但其内部的具体实现可以各异。这样我们就可以使用顶层类提供的统一接口来处理该层次的方法。
- 基于接口的实现表现为：不同的类实现接口，并覆盖接口中的同一个方法
  - 在接口的多态中，指向接口的引用 必须指定是 **实现了该接口的一个类的实例程序**，在运行时，根据对象引用的实际类型来执行对应的方法。
  - 继承都是单继承，只能为一组相关的类提供一致的服务接口。但是**接口可以是多继承多实现**，它能够利用一组相关或者不相关的接口进行组合与扩充，能够对外提供一致的服务接口。**所以它相对于继承来说有更好的灵活性**。



## 枚举类型enum

原文链接：https://blog.csdn.net/qq_31655965/article/details/55049192

Weekday.valueOf() 方法：

它的作用是传来一个字符串，然后将它转变为对应的枚举变量。前提是你传的字符串和定义枚举变量的字符串一抹一样，区分大小写。如果你传了一个不存在的字符串，那么会抛出异常。

Weekday.values()方法。

这个方法会返回包括所有枚举变量的数组。在该例中，返回的就是包含了七个星期的Weekday[]。可以方便的用来做循环。

枚举变量的toString()方法。

该方法直接返回枚举定义枚举变量的字符串，比如MON就返回【”MON”】。

枚举变量的.ordinal()方法。

默认请款下，枚举类会给所有的枚举变量一个默认的次序，该次序从0开始，类似于数组的下标。而.ordinal()方法就是获取这个次序（或者说下标）

枚举变量的compareTo()方法。

该方法用来比较两个枚举变量的”大小”，实际上比较的是两个枚举变量的次序，返回两个次序相减后的结果，如果为负数，就证明变量1”小于”变量2 （变量1.compareTo(变量2)，返回【变量1.ordinal() - 变量2.ordinal()】）



## Java常用关键字final,static,this,super总结

**final 关键字**

final关键字主要用在三个地方：变量、方法、类。

对于一个final变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。

当用final修饰一个类时，表明这个**类不能被继承**。final类中的所有成员方法都会被隐式地指定为final方法。

使用final方法的原因有两个。第一个原因是把方法锁定，以防任何继承类修改它的含义；第二个原因是效率。在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升（现在的Java版本已经不需要使用final方法进行这些优化了）。类中所有的private方法都隐式地指定为final。**该方法不能被重写**

**static 关键字**

static 关键字主要有以下四种使用场景：

修饰成员变量和成员方法: **被 static 修饰的成员属于类**，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static 声明的成员变量属于静态成员变量，静态变量 **存放在 Java 内存区域的方法区**。调用格式：类名.静态变量名 类名.静态方法名()
静态代码块: 静态代码块定义在类中方法外, 静态代码块在非静态代码块之前执行(静态代码块—>非静态代码块—>构造方法)。 该类不管创建多少对象，静态代码块只执行一次.
静态内部类（static修饰类的话只能修饰内部类）： 静态内部类与非静态内部类之间存在一个最大的区别: 非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有。没有这个引用就意味着：1. 它的创建是不需要依赖外围类的创建。2. 它不能使用任何外围类的非static成员变量和方法。
静态导包(用来导入类中的静态资源，1.5之后的新特性): 格式为：import static 这两个关键字连用可以指定导入某个类中的指定静态资源，并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法。

**this 关键字**

this关键字用于引用类的当前实例。 例如

**super 关键字**

super关键字用于从子类访问父类的变量和方法。

原文链接：https://blog.csdn.net/ljjzj/article/details/90639165

## 重写 重载

重载：方法名相同，但参数不同的多个同名函数

注意：1.参数不同的意思是参数类型、参数个数、参数顺序至少有一个不同

2.返回值和异常以及访问修饰符，不能作为重载的条件(因为对于匿名调用，会出现歧义，eg:void a ()和int a() ，如果调用a()，出现歧义)

3.main方法也是可以被重载的

覆盖：子类重写父类的方法，要求方法名和参数类型完全一样(参数不能是子类)，返回值和异常比父类小或者相同(即为父类的子类)，访问修饰符比父类大或者相同



## 抽象类和接口区别

(一) 继承方面：
       (1) 抽象类只能单继承；接口可以多实现
(二) 成员属性方面：
       (1) 抽象类中可以有普通属性，也可以有常量
       (2) 接口中的成员变量全部默认是常量，使用public static final修饰，这个可以省略不写
(三) 代码块方面：
       (1) 抽象类可以含初始化块；接口不能含初始化块
(四) 构造函数方面：
       (1) 接口不能有构造函数
       (2) 抽象类可以有构函数，但是这里的构造函数不是用来创建对象的，而是用来被实现类调用进行初始化操作的
(五) 方法方面：
       (1) 接口里面不能定义静态方法；抽象类里面可以定义静态方法
       (2) 接口里面只能是抽象方法；抽象类里面可以有抽象方法也可以有普通方法

上面就是接口与抽象类的区别，在说完区别之后，我们可以补充一下接口与抽象类之间的相同之处：
(1) 接口与抽象类都不能被实例化，需要被其他进行实现或继承
(2) 接口与抽象类里面都能包含抽象方法，实现接口或继承抽象类的子类都必须实现这些抽象方法
————————————————
版权声明：本文为CSDN博主「傻乎乎的熊二」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/wxw20147854/article/details/88712029

![image-20200629102526552](/Users/ran/Library/Application Support/typora-user-images/image-20200629102526552.png)

什么时候使用抽象类和接口

如果你拥有一些方法并且想让它们中的一些有默认实现，那么使用抽象类吧。 
如果你想实现多重继承，那么你必须使用接口。由于Java不支持多继承，子类不能够继承多个类，但可以实现多个接口。因此你就可以使用接口来解决它。 
如果基本功能在不断改变，那么就需要使用抽象类。如果不断改变基本功能并且使用接口，那么就需要改变所有实现了该接口的类。

## 反射机制

https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/basic/reflection.md



## HashMap

结构：

JDK1.8之前使用的是数组+链表的数据结构，每一个元素是一个Entry结点，包含key、value、hash值、指向下一个元素的next指针四个属性。JDK1.8之后使用的是数组+链表或红黑树的数据结构，每一个元素是一个Node结点，Node实现了Entry接口，Node有一个子类TreeNode，代表树结点。



[HashMap和HashTable区别](https://blog.csdn.net/Mrs_chens/article/details/93986400?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

**解决Hash冲突：**开放定址法、链地址法

**常见Hash算法：**

1）直接定址法 
取关键字或者关键字的某个线性函数为Hash地址，即Hash(key)=a*key+b

2）除留余数法 
如果知道Hash表的最大长度为m，可以取不大于m的最大质数p，然后对关键字进行取余运算，Hash(key)=key%p。 
在这里p的选取非常关键，p选择的好的话，能够最大程度地减少冲突，p一般取不大于m的最大质数。

3）平方取中法 
对关键字进行平方运算，然后取结果的中间几位作为Hash地址。假如有以下关键字序列{421，423，436}，平方之后的结果为{177241，178929，190096}，那么可以取{72，89，00}作为Hash地址。

4）折叠法 
将关键字拆分成几部分，然后将这几部分组合在一起，以特定的方式进行转化形成Hash地址。假如知道图书的ISBN号为8903-241-23，可以将Hash(key)=89+03+24+12+3作为Hash地址。
————————————————
版权声明：本文为CSDN博主「追梦者_AIer」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_30091945/article/details/78044445

**HashMap的时间复杂度是O(1)**

https://blog.csdn.net/li_huai_dong/article/details/79910626

**HashMap 1.7,1.8区别**

**头插法、尾插法**

JDK1.7是用单链表进行的纵向延伸，当采用头插法时会容易出现逆序且环形链表死循环问题。但是在JDK1.8之后是因为加入了红黑树使用尾插法，能够避免出现逆序且链表死循环的问题。

**扩容后的存储位置**

1. 在JDK1.7的时候是直接用hash值和需要扩容的二进制数进行&（这里就是为什么扩容的时候为啥一定必须是2的多少次幂的原因所在，因为如果只有2的n次幂的情况时最后一位二进制数才一定是1，这样能最大程度减少hash碰撞）（hash值 & length-1）

2、而在JDK1.8的时候直接用了JDK1.7的时候计算的规律，也就是扩容前的原始位置+扩容的大小值=JDK1.8的计算方式，而不再是JDK1.7的那种异或的方法。但是这种方式就相当于只需要判断Hash值的新增参与运算的位是0还是1就直接迅速计算出了扩容后的储存方式。

**红黑树结构**

https://blog.csdn.net/qq_36520235/article/details/82417949?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

https://blog.csdn.net/woshimaxiao1/article/details/83661464



### jdk1.8中的hashmap.put方法

我们在使用put方法的时候会传进key和value参数

在我们将这两个参数传入后，

第一步，我们的put方法会去判断这个hashmap是否为null 或者长度是否为0，

若为null或者长度为0 则新建一个（这也是平时在编程过程中需要经常注意的细节），

第二步，就用到了我们这个key值啦，put方法会根据这个key计算hash码来得到数组的位置，

```
数组位置计算方法：
①在存放数据时会先通过hash方法计算key的hashCode，JDK1.8之前的计算比较复杂，但是效率并不高，JDK1.8将计算出的hashCode高低16位进行异或运算，可以保证尽可能多的位数参与运算，并且让结果中的0和1尽量分布均匀，降低哈希冲突的概率，使键值尽可能分散，提高查询效率。
②计算出hash值后，再将hash值与数组的长度-1进行与操作，这样可以保证索引的范围在数组的范围之内，由于数组长度必须是2的幂次方，-1后必然是011..11这样的形式，进行与运算就可以保证结果的0和1分别更加均匀。
```

（这里需要解释一下，我们的hashmap默认是由一个数组加链表组成的）

得到位置后当然是继续判断这个数组下标的值是否为null，

为null 自然是直接插入我们的value值，else

第三步，判断key是否存在，当key！=null我们就可以覆盖value值，else if

第四步，判断数组后面跟着的这个链是否为树（TreeNode），是树呢，我们传入的值就会按照key，value的格式存入了，else

第五步，不是树就是链表，那么put方法就会遍历这个链表，

第六步，在遍历的时候呢我们会判断这个链表的长度是否大于8，大于呢就会将这个链表转换为树，再按照key，value的格式存入

```
达到建树阈值TREEIFY_THRESHOLD-1时，就会将链表转为红黑树，TREEIFY_THRESHOLD是一个值为8常量。由于链表查找时间复杂度为O(n)，红黑树为O(logn)，当数值太小时查找效率相差无几，因此设有一个阈值。
```

第七步，小于则会判断链表中的key！=null，若key！=null则覆盖，key==null我们的value就会插入

最后一步为判断扩容，当数组容量超过最大容量时就会扩容一倍（即二进制的进位）

![img](https://images2018.cnblogs.com/blog/1331009/201802/1331009-20180226182031105-2007285957.png)————————————————

版权声明：本文为CSDN博主「JumpG」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_38480293/article/details/79405352



### 扩容因子为啥是0.75

加载因子过高，例如为1，虽然减少了空间开销，提高了空间利用率，但同时也增加了查询时间成本；

**加载因子过低，例如0.5，虽然可以减少查询时间成本，但是空间利用率很低，同时提高了rehash操作的次数**。

**在设置初始容量时应该考虑到映射中所需的条目数及其加载因子，以便最大限度地减少rehash操作次数，所以，一般在使用HashMap时建议根据预估值设置初始容量，减少扩容操作。**

**选择0.75作为默认的加载因子，完全是时间和空间成本上寻求的一种折衷选择，** 





### resize方法：

①重新规划table的长度和阈值，如果达到扩容阈值，就把table的容量增加到旧容量的2倍。如果新的容量小于默认的初始化容量16就置为16，阈值重新设置为新容量和加载因子之积。如果新的table容量超出或等于最大容量(1<<30)，将阈值调整为最大整形数，并且return终止过程。
②重新排列数据结点，遍历table上的每一个结点分别处理。如果是null则跳过，如果不为null且没有next结点，重新计算hash值并存入新的table。如果结点为树结点，调用split方法处理，如果红黑树太小就退化回链表。如果都不是，则说明是链表结点，如果hash值和oldCap与的结果为0则不处理，否则存放到新的下标。

### key value 回收

1.如果有一个值，对应的键不再使用他了，但由于key与value之间存在**强引用**，是不会被垃圾回收的 
2.垃圾回收器跟踪活动的对象，只要映射对象是活动的，其中的所有桶也是活动的，它们不能被回收 

## HashSet底层实现

用hashmap实现

https://blog.csdn.net/HD243608836/article/details/80214413/

## LinkedHashMap与HashMap的区别

**HashMap**

- Map存储过程：计算key的hashCode值，确定位置；如果位置上有元素，用equals判断是否一致，如果一致，不存，如果不一致，遍历下一个节点继续判断equals。注：添加是添加到链表的尾部。
- 加载因子（扩容条件）：默认0.75，空间存储75%后扩容。
  扩容：将原来的元素重新计算位置再存入；计算需要时间，因此不可以频繁扩容，扩容是成倍的。
- HashMap根据键可以很快找到他的值，因此具有很快的访问速度，遍历时，取得数据的顺序是完全随机的。
- HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap;可能会导致数据的不一致。
- HashMap的键只允许一条为null，值可以多个为null

**LinkedHashMap——有序的Map**

- 使用Map接口的哈希表和链表实现，具有可预知的迭代顺序。此实现与HashMap的不同之处在于：LinkedHashMap维护着一个双向循环链表。此链表定义了迭代顺序，该迭代顺序通常就是存放元素的顺序。
- 维护使用排序，最近使用的会移至尾部，例如 M1 M2 M3 M4，使用M3后为 M1 M2 M4 M3了，LinkedHashMap输出时其元素是有顺序的，而HashMap输出时是随机的，如果Map映射比较复杂而又要求高效率的话，最好使用LinkedHashMap，但是多线程访问的话可能会造成不同步，所以要用Collections.synchronizedMap来包装一下，从而实现同步。另外，LinkedHashMap可以实现快速的查询第一个元素（First）跟结尾（Last）。
- 遍历速度比HashMap慢
  

## TreeMap和HashMap区别

　　TreeMap取出来的是排序后的键值对。但如果您要按自然顺序或自定义顺序遍历键，那么TreeMap会更好 。



## 深拷贝 浅拷贝

### 创建对象的5种方式

　　**①、通过 new 关键字**

　　这是最常用的一种方式，通过 new 关键字调用类的有参或无参构造方法来创建对象。比如 Object obj = new Object();

　　**②、通过 Class 类的 newInstance() 方法**

　　这种默认是调用类的无参构造方法创建对象。比如 Person p2 = (Person) Class.forName("com.ys.test.Person").newInstance();

　　**③、通过 Constructor 类的 newInstance 方法**

　　这和第二种方法类时，都是通过反射来实现。通过 java.lang.relect.Constructor 类的 newInstance() 方法指定某个构造器来创建对象。

　　Person p3 = (Person) Person.class.getConstructors()[0].newInstance();

　　实际上第二种方法利用 Class 的 newInstance() 方法创建对象，其内部调用还是 Constructor 的 newInstance() 方法。

　　**④、利用 Clone 方法**

　　Clone 是 Object 类中的一个方法，通过 对象A.clone() 方法会创建一个内容和对象 A 一模一样的对象 B，clone 克隆，顾名思义就是创建一个一模一样的对象出来。

　　Person p4 = (Person) p3.clone();

　　**⑤、反序列化**

　　序列化是把堆内存中的 Java 对象数据，通过某种方式把对象存储到磁盘文件中或者传递给其他网络节点（在网络上传输）。而反序列化则是把磁盘文件中的对象数据或者把网络节点上的对象数据，恢复成Java对象模型的过程。

### 基本类型和引用类型

　　在 Java 中数据类型可以分为两大类：基本类型和引用类型。

　　基本类型也称为值类型，分别是字符类型 char，布尔类型 boolean以及数值类型 byte、short、int、long、float、double。

　　引用类型则包括类、接口、数组、枚举等。

　　Java 将内存空间分为堆和栈。基本类型直接在栈中存储数值，而引用类型是将引用放在栈中，实际存储的值是放在堆中，通过栈中的引用指向堆中存放的数据。

　　![img](https://images2018.cnblogs.com/blog/1120165/201803/1120165-20180312213707709-1454308742.png)

　　上图定义的 a 和 b 都是基本类型，其值是直接存放在栈中的；而 c 和 d 是 String 声明的，这是一个引用类型，引用地址是存放在 栈中，然后指向堆的内存空间。

　　下面 d = c；这条语句表示将 c 的引用赋值给 d，那么 c 和 d 将指向同一块堆内存空间。

### 浅拷贝

　**浅拷贝：创建一个新对象，然后将当前对象的非静态字段复制到该新对象，如果字段是值类型的，那么对该字段执行复制；如果该字段是引用类型的话，则复制引用但不复制引用的对象。因此，原始对象及其副本引用同一个对象。**

注意：调用对象的 clone 方法，必须要让类实现 Cloneable 接口，并且覆写 clone 方法。

我们看如下这段代码：

```java
package com.ys.test;

public class Person implements Cloneable{
    public String pname;
    public int page;
    public Address address;
    public Person() {}
    
    public Person(String pname,int page){
        this.pname = pname;
        this.page = page;
        this.address = new Address();
    }
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
    
    public void setAddress(String provices,String city ){
        address.setAddress(provices, city);
    }
    public void display(String name){
        System.out.println(name+":"+"pname=" + pname + ", page=" + page +","+ address);
    }

    public String getPname() {
        return pname;
    }

    public void setPname(String pname) {
        this.pname = pname;
    }

    public int getPage() {
        return page;
    }

    public void setPage(int page) {
        this.page = page;
    }
    
}
```

```java
package com.ys.test;

public class Address {
    private String provices;
    private String city;
    public void setAddress(String provices,String city){
        this.provices = provices;
        this.city = city;
    }
    @Override
    public String toString() {
        return "Address [provices=" + provices + ", city=" + city + "]";
    }
    
}
```

　　这是一个我们要进行赋值的原始类 Person。下面我们产生一个 Person 对象，并调用其 clone 方法复制一个新的对象。

　　测试：

```java
@Test
public void testShallowClone() throws Exception{
    Person p1 = new Person("zhangsan",21);
    p1.setAddress("湖北省", "武汉市");
    Person p2 = (Person) p1.clone();
    System.out.println("p1:"+p1);
    System.out.println("p1.getPname:"+p1.getPname().hashCode());
    
    System.out.println("p2:"+p2);
    System.out.println("p2.getPname:"+p2.getPname().hashCode());
    
    p1.display("p1");
    p2.display("p2");
    p2.setAddress("湖北省", "荆州市");
    System.out.println("将复制之后的对象地址修改：");
    p1.display("p1");
    p2.display("p2");
}
```

　　打印结果为：

　　![img](https://images2018.cnblogs.com/blog/1120165/201803/1120165-20180312214947767-1020527476.png)

　　首先看原始类 Person 实现 Cloneable 接口，并且覆写 clone 方法,它还有三个属性，一个引用类型 String定义的 pname，一个基本类型 int定义的 page，还有一个引用类型 Address ，这是一个自定义类，这个类也包含两个属性 pprovices 和 city 。

　　接着看测试内容，首先我们创建一个Person 类的对象 p1，其pname 为zhangsan,page为21，地址类 Address 两个属性为 湖北省和武汉市。接着我们调用 clone() 方法复制另一个对象 p2，接着打印这两个对象的内容。

　　从第 1 行和第 3 行打印结果:

　　p1:com.ys.test.Person@349319f9

　　p2:com.ys.test.Person@258e4566

　　可以看出这是两个不同的对象。

　　从第 5 行和第 6 行打印的对象内容看，原对象 p1 和克隆出来的对象 p2 内容完全相同。

　　代码中我们只是更改了克隆对象 p2 的属性 Address 为湖北省荆州市（原对象 p1 是湖北省武汉市） ，但是从第 7 行和第 8 行打印结果来看，原对象 p1 和克隆对象 p2 的 Address 属性都被修改了。

　　也就是说对象 Person 的属性 Address，经过 clone 之后，其实只是复制了其引用，他们指向的还是同一块堆内存空间，当修改其中一个对象的属性 Address，另一个也会跟着变化。

　　![img](https://images2018.cnblogs.com/blog/1120165/201803/1120165-20180312220935185-85540133.png)

### 深拷贝

　　弄清楚了浅拷贝，那么深拷贝就很容易理解了。

　　**深拷贝：创建一个新对象，然后将当前对象的非静态字段复制到该新对象，无论该字段是值类型的还是引用类型，都复制独立的一份。当你修改其中一个对象的任何内容时，都不会影响另一个对象的内容。**

　　![img](https://images2018.cnblogs.com/blog/1120165/201803/1120165-20180313205221201-187008977.png)

　　那么该如何实现深拷贝呢？**Object 类提供的 clone 是只能实现 浅拷贝的。**

### 如何实现深拷贝？

　　深拷贝的原理我们知道了，就是要让原始对象和克隆之后的对象所具有的引用类型属性不是指向同一块堆内存，这里有三种实现思路。

#### 　　①、让每个引用类型属性内部都重写clone() 方法

　　既然引用类型不能实现深拷贝，那么我们将每个引用类型都拆分为基本类型，分别进行浅拷贝。比如上面的例子，Person 类有一个引用类型 Address(其实String 也是引用类型，但是String类型有点特殊，后面会详细讲解)，我们在 Address 类内部也重写 clone 方法。如下：

　　Address.class:

```java
 1 package com.ys.test;
 2 
 3 public class Address implements Cloneable{
 4     private String provices;
 5     private String city;
 6     public void setAddress(String provices,String city){
 7         this.provices = provices;
 8         this.city = city;
 9     }
10     @Override
11     public String toString() {
12         return "Address [provices=" + provices + ", city=" + city + "]";
13     }
14     @Override
15     protected Object clone() throws CloneNotSupportedException {
16         return super.clone();
17     }
18     
19 }
```

　　Person.class 的 clone() 方法：

```java
1     @Override
2     protected Object clone() throws CloneNotSupportedException {
3         Person p = (Person) super.clone();
4         p.address = (Address) address.clone();
5         return p;
6     }
```

　　测试还是和上面一样，我们会发现更改了p2对象的Address属性，p1 对象的 Address 属性并没有变化。

　　但是这种做法有个弊端，这里我们Person 类只有一个 Address 引用类型，而 Address 类没有，所以我们只用重写 Address 类的clone 方法，但是如果 Address 类也存在一个引用类型，那么我们也要重写其clone 方法，这样下去，有多少个引用类型，我们就要重写多少次，如果存在很多引用类型，那么代码量显然会很大，所以这种方法不太合适。

#### 　　②、利用序列化

　　序列化是将对象写到流中便于传输，而反序列化则是把对象从流中读取出来。这里写到流中的对象则是原始对象的一个拷贝，因为原始对象还存在 JVM 中，所以我们可以利用对象的序列化产生克隆对象，然后通过反序列化获取这个对象。

　　注意每个需要序列化的类都要实现 Serializable 接口，如果有某个属性不需要序列化，可以将其声明为 transient，即将其排除在克隆属性之外。

```java
//深度拷贝
public Object deepClone() throws Exception{
    // 序列化
    ByteArrayOutputStream bos = new ByteArrayOutputStream();
    ObjectOutputStream oos = new ObjectOutputStream(bos);

    oos.writeObject(this);

    // 反序列化
    ByteArrayInputStream bis = new ByteArrayInputStream(bos.toByteArray());
    ObjectInputStream ois = new ObjectInputStream(bis);

    return ois.readObject();
}
```

 　因为序列化产生的是两个完全独立的对象，所有无论嵌套多少个引用类型，序列化都是能实现深拷贝的。



## 四种引用

在 JDK.1.2 之后，Java 对引用的概念进行了扩充，将引用分为了：强引用（Strong Reference）、软引用（Soft Reference）、弱引用（Weak Reference）、虚引用（Phantom Reference）4 种，这 4 种引用的强度依次减弱。

### 一，强引用

Java中默认声明的就是强引用，比如：

```
Object obj = new Object(); //只要obj还指向Object对象，Object对象就不会被回收
obj = null;  //手动置null
```

只要强引用存在，垃圾回收器将永远不会回收被引用的对象，哪怕内存不足时，JVM也会直接抛出OutOfMemoryError，不会去回收。如果想中断强引用与对象之间的联系，可以显示的将强引用赋值为null，这样一来，JVM就可以适时的回收对象了

### 二，软引用

软引用是用来描述一些非必需但仍有用的对象。**在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常**。这种特性常常被用来实现缓存技术，比如网页缓存，图片缓存等。
在 JDK1.2 之后，用java.lang.ref.SoftReference类来表示软引用。

下面以一个例子来进一步说明强引用和软引用的区别：
在运行下面的Java代码之前，需要先配置参数 -Xms2M -Xmx3M，将 JVM 的初始内存设为2M，最大可用内存为 3M。

首先先来测试一下强引用，在限制了 JVM 内存的前提下，下面的代码运行正常

```
public class TestOOM {
	
	public static void main(String[] args) {
		 testStrongReference();
	}
	private static void testStrongReference() {
		// 当 new byte为 1M 时，程序运行正常
		byte[] buff = new byte[1024 * 1024 * 1];
	}
}
```

但是如果我们将

```
byte[] buff = new byte[1024 * 1024 * 1];
```

替换为创建一个大小为 2M 的字节数组

```
byte[] buff = new byte[1024 * 1024 * 2];
```

则内存不够使用，程序直接报错，强引用并不会被回收
![img](https://img2018.cnblogs.com/blog/662236/201809/662236-20180922194052676-1646914311.png)

接着来看一下软引用会有什么不一样，在下面的示例中连续创建了 10 个大小为 1M 的字节数组，并赋值给了软引用，然后循环遍历将这些对象打印出来。

```
public class TestOOM {
	private static List<Object> list = new ArrayList<>();
	public static void main(String[] args) {
	     testSoftReference();
	}
	private static void testSoftReference() {
		for (int i = 0; i < 10; i++) {
			byte[] buff = new byte[1024 * 1024];
			SoftReference<byte[]> sr = new SoftReference<>(buff);
			list.add(sr);
		}
		
		System.gc(); //主动通知垃圾回收
		
		for(int i=0; i < list.size(); i++){
			Object obj = ((SoftReference) list.get(i)).get();
			System.out.println(obj);
		}
		
	}
	
}
```

打印结果：
![img](https://img2018.cnblogs.com/blog/662236/201809/662236-20180922194016719-117632363.png)

我们发现无论循环创建多少个软引用对象，打印结果总是只有最后一个对象被保留，其他的obj全都被置空回收了。
这里就说明了在内存不足的情况下，软引用将会被自动回收。
值得注意的一点 , 即使有 byte[] buff 引用指向对象, 且 buff 是一个strong reference, 但是 SoftReference sr 指向的对象仍然被回收了，这是因为Java的编译器发现了在之后的代码中, buff 已经没有被使用了, 所以自动进行了优化。
如果我们将上面示例稍微修改一下：

```
	private static void testSoftReference() {
		byte[] buff = null;

		for (int i = 0; i < 10; i++) {
			buff = new byte[1024 * 1024];
			SoftReference<byte[]> sr = new SoftReference<>(buff);
			list.add(sr);
		}

        System.gc(); //主动通知垃圾回收
		
		for(int i=0; i < list.size(); i++){
			Object obj = ((SoftReference) list.get(i)).get();
			System.out.println(obj);
		}

		System.out.println("buff: " + buff.toString());
	}
```

则 buff 会因为强引用的存在，而无法被垃圾回收，从而抛出OOM的错误。
![img](https://img2018.cnblogs.com/blog/662236/201809/662236-20180922194030314-105853688.png)

如果一个对象惟一剩下的引用是软引用，那么该对象是软可及的（softly reachable）。垃圾收集器并不像其收集弱可及的对象一样尽量地收集软可及的对象，相反，它只在真正 “需要” 内存时才收集软可及的对象。

### 三，弱引用

弱引用的引用强度比软引用要更弱一些，**无论内存是否足够，只要 JVM 开始进行垃圾回收，那些被弱引用关联的对象都会被回收**。在 JDK1.2 之后，用 java.lang.ref.WeakReference 来表示弱引用。
我们以与软引用同样的方式来测试一下弱引用：

```
	private static void testWeakReference() {
		for (int i = 0; i < 10; i++) {
			byte[] buff = new byte[1024 * 1024];
			WeakReference<byte[]> sr = new WeakReference<>(buff);
			list.add(sr);
		}
		
		System.gc(); //主动通知垃圾回收
		
		for(int i=0; i < list.size(); i++){
			Object obj = ((WeakReference) list.get(i)).get();
			System.out.println(obj);
		}
	}
```

打印结果：
![img](https://img2018.cnblogs.com/blog/662236/201809/662236-20180922194112309-477100844.png)

可以发现所有被弱引用关联的对象都被垃圾回收了。

### 四，虚引用

虚引用是最弱的一种引用关系，如果一个对象仅持有虚引用，那么它就和没有任何引用一样，它随时可能会被回收，在 JDK1.2 之后，用 PhantomReference 类来表示，通过查看这个类的源码，发现它只有一个构造函数和一个 get() 方法，而且它的 get() 方法仅仅是返回一个null，也就是说将永远无法通过虚引用来获取对象，虚引用必须要和 ReferenceQueue 引用队列一起使用。

```
public class PhantomReference<T> extends Reference<T> {
    /**
     * Returns this reference object's referent.  Because the referent of a
     * phantom reference is always inaccessible, this method always returns
     * <code>null</code>.
     *
     * @return  <code>null</code>
     */
    public T get() {
        return null;
    }
    public PhantomReference(T referent, ReferenceQueue<? super T> q) {
        super(referent, q);
    }
}
```

那么传入它的构造方法中的 ReferenceQueue 又是如何使用的呢？

### 五，引用队列（ReferenceQueue）

引用队列可以与软引用、弱引用以及虚引用一起配合使用，当垃圾回收器准备回收一个对象时，如果发现它还有引用，那么就会在回收对象之前，把这个引用加入到与之关联的引用队列中去。程序可以通过判断引用队列中是否已经加入了引用，来判断被引用的对象是否将要被垃圾回收，这样就可以在对象被回收之前采取一些必要的措施。

与软引用、弱引用不同，虚引用必须和引用队列一起使用。

## 网上整理常见问题

### 语言特性 12

#### Q1：Java 语言的优点？

① 平台无关性，摆脱硬件束缚，"一次编写，到处运行"。

② 相对安全的内存管理和访问机制，避免大部分内存泄漏和指针越界。

③ 热点代码检测和运行时编译及优化，使程序随运行时间增长获得更高性能。

④ 完善的应用程序接口，支持第三方类库。

------

#### Q2：Java 如何实现平台无关？

**JVM：** Java 编译器可生成与计算机体系结构无关的字节码指令，字节码文件不仅可以轻易地在任何机器上解释执行，还可以动态地转换成本地机器代码，转换是由 JVM 实现的，JVM 是平台相关的，屏蔽了不同操作系统的差异。

**语言规范：** 基本数据类型大小有明确规定，例如 int 永远为 32 位，而 C/C++ 中可能是 16 位、32 位，也可能是编译器开发商指定的其他大小。Java 中数值类型有固定字节数，二进制数据以固定格式存储和传输，字符串采用标准的 Unicode 格式存储。

------

#### Q3：JDK 和 JRE 的区别？

**JDK：** Java Development Kit，开发工具包。提供了编译运行 Java 程序的各种工具，包括编译器、JRE 及常用类库，是 JAVA 核心。

**JRE：** Java Runtime Environment，运行时环境，运行 Java 程序的必要环境，包括 JVM、核心类库、核心配置工具。

------

#### Q4：Java 按值调用还是引用调用？

**按值调用**指方法接收调用者提供的值，**按引用调用**指方法接收调用者提供的变量地址。

Java 总是按值调用，方法得到的是所有参数值的副本，传递对象时实际上方法接收的是对象引用的副本。方法不能修改基本数据类型的参数，如果传递了一个 int 值 ，改变值不会影响实参，因为改变的是值的一个副本。

可以改变对象参数的状态，但不能让对象参数引用一个新的对象。如果传递了一个 int 数组，改变数组的内容会影响实参，而改变这个参数的引用并不会让实参引用新的数组对象。

------

#### Q5：浅拷贝和深拷贝的区别？

**浅拷贝：** 只复制当前对象的基本数据类型及引用变量，没有复制引用变量指向的实际对象。修改克隆对象可能影响原对象，不安全。

**深拷贝：** 完全拷贝基本数据类型和引用数据类型，安全。

------

#### Q6：什么是反射？

在运行状态中，对于任意一个类都能知道它的所有属性和方法，对于任意一个对象都能调用它的任意方法和属性，这种动态获取信息及调用对象方法的功能称为反射。缺点是破坏了封装性以及泛型约束。反射是框架的核心，Spring 大量使用反射。

------

#### Q7：Class 类的作用？如何获取一个 Class 对象？

在程序运行期间，Java 运行时系统为所有对象维护一个运行时类型标识，这个信息会跟踪每个对象所属的类，虚拟机利用运行时类型信息选择要执行的正确方法，保存这些信息的类就是 Class，这是一个泛型类。

获取 Class 对象：① `类名.class` 。②对象的 `getClass`方法。③ `Class.forName(类的全限定名)`。

------

#### Q8：什么是注解？什么是元注解？

**注解**是一种标记，使类或接口附加额外信息，帮助编译器和 JVM 完成一些特定功能，例如 `@Override` 标识一个方法是重写方法。

**元注解**是自定义注解的注解，例如：

`@Target`：约束作用位置，值是 ElementType 枚举常量，包括 METHOD 方法、VARIABLE 变量、TYPE 类/接口、PARAMETER 方法参数、CONSTRUCTORS 构造方法和 LOACL_VARIABLE 局部变量等。

`@Rentention`：约束生命周期，值是 RetentionPolicy 枚举常量，包括 SOURCE 源码、CLASS 字节码和 RUNTIME 运行时。

`@Documented`：表明这个注解应该被 javadoc 记录。

------

#### Q9：什么是泛型，有什么作用？

**泛型**本质是参数化类型，解决不确定对象具体类型的问题。泛型在定义处只具备执行 Object 方法的能力。

泛型的好处：① 类型安全，放置什么出来就是什么，不存在 ClassCastException。② 提升可读性，编码阶段就显式知道泛型集合、泛型方法等处理的对象类型。③ 代码重用，合并了同类型的处理代码。

#### Q10：泛型擦除是什么？

泛型用于编译阶段，编译后的字节码文件不包含泛型类型信息，因为虚拟机没有泛型类型对象，所有对象都属于普通类。例如定义 `List<Object>` 或 `List<String>`，在编译后都会变成 `List` 。

定义一个泛型类型，会自动提供一个对应原始类型，类型变量会被擦除。如果没有限定类型就会替换为 Object，如果有限定类型就会替换为第一个限定类型，例如 `<T extends A & B>` 会使用 A 类型替换 T。

------

#### Q11：JDK8 新特性有哪些？

**lambda 表达式：**允许把函数作为参数传递到方法，简化匿名内部类代码。

**函数式接口：**使用 `@FunctionalInterface` 标识，有且仅有一个抽象方法，可被隐式转换为 lambda 表达式。

**方法引用：**可以引用已有类或对象的方法和构造方法，进一步简化 lambda 表达式。

**接口：**接口可以定义 `default` 修饰的默认方法，降低了接口升级的复杂性，还可以定义静态方法。

**注解：**引入重复注解机制，相同注解在同地方可以声明多次。注解作用范围也进行了扩展，可作用于局部变量、泛型、方法异常等。

**类型推测：**加强了类型推测机制，使代码更加简洁。

**Optional 类：**处理空指针异常，提高代码可读性。

**Stream 类：**引入函数式编程风格，提供了很多功能，使代码更加简洁。方法包括 `forEach` 遍历、`count` 统计个数、`filter` 按条件过滤、`limit` 取前 n 个元素、`skip` 跳过前 n 个元素、`map` 映射加工、`concat` 合并 stream 流等。

**日期：**增强了日期和时间 API，新的 java.time 包主要包含了处理日期、时间、日期/时间、时区、时刻和时钟等操作。

**JavaScript：**提供了一个新的 JavaScript 引擎，允许在 JVM上运行特定 JavaScript 应用。

------

#### Q12：异常有哪些分类？

所有异常都是 Throwable 的子类，分为 Error 和 Exception。**Error** 是 Java 运行时系统的内部错误和资源耗尽错误，例如 StackOverFlowError 和 OutOfMemoryError，这种异常程序无法处理。

**Exception** 分为受检异常和非受检异常，受检异常需要在代码中显式处理，否则会编译出错，非受检异常是运行时异常，继承自 RuntimeException。

**受检异常**：① 无能为力型，如字段超长导致的 SQLException。② 力所能及型，如未授权异常 UnAuthorizedException，程序可跳转权限申请页面。常见受检异常还有 FileNotFoundException、ClassNotFoundException、IOException等。

**非受检异常**：① 可预测异常，例如 IndexOutOfBoundsException、NullPointerException、ClassCastException 等，这类异常应该提前处理。② 需捕捉异常，例如进行 RPC 调用时的远程服务超时，这类异常客户端必须显式处理。③ 可透出异常，指框架或系统产生的且会自行处理的异常，例如 Spring 的 NoSuchRequestHandingMethodException，Spring 会自动完成异常处理，将异常自动映射到合适的状态码。

------

### 数据类型 5

#### Q1：Java 有哪些基本数据类型？

| 数据类型 | 内存大小                               | 默认值   | 取值范围                    |
| -------- | -------------------------------------- | -------- | --------------------------- |
| byte     | 1 B                                    | (byte)0  | -128 ~ 127                  |
| short    | 2 B                                    | (short)0 | -2^15^ ~ 2^15^-1            |
| int      | 4 B                                    | 0        | -2^31^ ~ 2^31^-1            |
| long     | 8 B                                    | 0L       | -2^63^ ~ 2^63^-1            |
| float    | 4 B                                    | 0.0F     | ±3.4E+38（有效位数 6~7 位） |
| double   | 8 B                                    | 0.0D     | ±1.7E+308（有效位数 15 位） |
| char     | 英文 1B，中文 UTF-8 占 3B，GBK 占 2B。 | '\u0000' | '\u0000' ~ '\uFFFF'         |
| boolean  | 单个变量 4B / 数组 1B                  | false    | true、false                 |

JVM 没有 boolean 赋值的专用字节码指令，`boolean f = false` 就是使用 ICONST_0 即常数 0 赋值。单个 boolean 变量用 int 代替，boolean 数组会编码成 byte 数组。

------

#### Q2：自动装箱/拆箱是什么？

每个基本数据类型都对应一个包装类，除了 int 和 char 对应 Integer 和 Character 外，其余基本数据类型的包装类都是首字母大写即可。

**自动装箱：** 将基本数据类型包装为一个包装类对象，例如向一个泛型为 Integer 的集合添加 int 元素。

**自动拆箱：** 将一个包装类对象转换为一个基本数据类型，例如将一个包装类对象赋值给一个基本数据类型的变量。

比较两个包装类数值要用 `equals` ，而不能用 `==` 。

------

#### Q3：String 是不可变类为什么值可以修改？

String 类和其存储数据的成员变量 value 字节数组都是 final 修饰的。对一个 String 对象的任何修改实际上都是创建一个新 String 对象，再引用该对象。只是修改 String 变量引用的对象，没有修改原 String 对象的内容。

------

#### Q4：字符串拼接的方式有哪些？

① 直接用 `+` ，底层用 StringBuilder 实现。只适用小数量，如果在循环中使用 `+` 拼接，相当于不断创建新的 StringBuilder 对象再转换成 String 对象，效率极差。

② 使用 String 的 concat 方法，该方法中使用 `Arrays.copyOf` 创建一个新的字符数组 buf 并将当前字符串 value 数组的值拷贝到 buf 中，buf 长度 = 当前字符串长度 + 拼接字符串长度。之后调用 `getChars` 方法使用 `System.arraycopy` 将拼接字符串的值也拷贝到 buf 数组，最后用 buf 作为构造参数 new 一个新的 String 对象返回。效率稍高于直接使用 `+`。

③ 使用 StringBuilder 或 StringBuffer，两者的 `append` 方法都继承自 AbstractStringBuilder，该方法首先使用 `Arrays.copyOf` 确定新的字符数组容量，再调用 `getChars` 方法使用 `System.arraycopy` 将新的值追加到数组中。StringBuilder 是 JDK5 引入的，效率高但线程不安全。StringBuffer 使用 synchronized 保证线程安全。

------

#### Q5：String a = "a" + new String("b") 创建了几个对象？

常量和常量拼接仍是常量，结果在常量池，只要有变量参与拼接结果就是变量，存在堆。

使用字面量时只创建一个常量池中的常量，使用 new 时如果常量池中没有该值就会在常量池中新创建，再在堆中创建一个对象引用常量池中常量。因此 `String a = "a" + new String("b")` 会创建四个对象，常量池中的 a 和 b，堆中的 b 和堆中的 ab。

------

### 面向对象 10

#### Q1：谈一谈你对面向对象的理解

面向过程让计算机有步骤地顺序做一件事，是过程化思维，使用面向过程语言开发大型项目，软件复用和维护存在很大问题，模块之间耦合严重。面向对象相对面向过程更适合解决规模较大的问题，可以拆解问题复杂度，对现实事物进行抽象并映射为开发对象，更接近人的思维。

例如开门这个动作，面向过程是 `open(Door door)`，动宾结构，door 作为操作对象的参数传入方法，方法内定义开门的具体步骤。面向对象的方式首先会定义一个类 Door，抽象出门的属性（如尺寸、颜色）和行为（如 open 和 close），主谓结构。

面向过程代码松散，强调流程化解决问题。面向对象代码强调高内聚、低耦合，先抽象模型定义共性行为，再解决实际问题。

------

#### Q2：面向对象的三大特性？

**封装**是对象功能内聚的表现形式，在抽象基础上决定信息是否公开及公开等级，核心问题是以什么方式暴漏哪些信息。主要任务是对属性、数据、敏感行为实现隐藏，对属性的访问和修改必须通过公共接口实现。封装使对象关系变得简单，降低了代码耦合度，方便维护。

迪米特原则就是对封装的要求，即 A 模块使用 B 模块的某接口行为，对 B 模块中除此行为外的其他信息知道得应尽可能少。不直接对 public 属性进行读取和修改而使用 getter/setter 方法是因为假设想在修改属性时进行权限控制、日志记录等操作，在直接访问属性的情况下无法实现。如果将 public 的属性和行为修改为 private 一般依赖模块都会报错，因此不知道使用哪种权限时应优先使用 private。

**继承**用来扩展一个类，子类可继承父类的部分属性和行为使模块具有复用性。继承是"is-a"关系，可使用里氏替换原则判断是否满足"is-a"关系，即任何父类出现的地方子类都可以出现。如果父类引用直接使用子类引用来代替且可以正确编译并执行，输出结果符合子类场景预期，那么说明两个类符合里氏替换原则。

**多态**以封装和继承为基础，根据运行时对象实际类型使同一行为具有不同表现形式。多态指在编译层面无法确定最终调用的方法体，在运行期由 JVM 动态绑定，调用合适的重写方法。由于重载属于静态绑定，本质上重载结果是完全不同的方法，因此多态一般专指重写。

------

#### Q3：重载和重写的区别？

**重载**指方法名称相同，但参数类型个数不同，是行为水平方向不同实现。对编译器来说，方法名称和参数列表组成了一个唯一键，称为方法签名，JVM 通过方法签名决定调用哪种重载方法。不管继承关系如何复杂，重载在编译时可以根据规则知道调用哪种目标方法，因此属于静态绑定。

JVM 在重载方法中选择合适方法的顺序：① 精确匹配。② 基本数据类型自动转换成更大表示范围。③ 自动拆箱与装箱。④ 子类向上转型。⑤ 可变参数。

**重写**指子类实现接口或继承父类时，保持方法签名完全相同，实现不同方法体，是行为垂直方向不同实现。

元空间有一个方法表保存方法信息，如果子类重写了父类的方法，则方法表中的方法引用会指向子类实现。父类引用执行子类方法时无法调用子类存在而父类不存在的方法。

重写方法访问权限不能变小，返回类型和抛出的异常类型不能变大，必须加 `@Override` 。

------

#### Q4：类之间有哪些关系？

| 类关系 | 描述                           | 权力强侧 | 举例                             |
| ------ | ------------------------------ | -------- | -------------------------------- |
| 继承   | 父子类之间的关系：is-a         | 父类     | 小狗继承于动物                   |
| 实现   | 接口和实现类之间的关系：can-do | 接口     | 小狗实现了狗叫接口               |
| 组合   | 比聚合更强的关系：contains-a   | 整体     | 头是身体的一部分                 |
| 聚合   | 暂时组装的关系：has-a          | 组装方   | 小狗和绳子是暂时的聚合关系       |
| 依赖   | 一个类用到另一个：depends-a    | 被依赖方 | 人养小狗，人依赖于小狗           |
| 关联   | 平等的使用关系：links-a        | 平等     | 人使用卡消费，卡可以提取人的信息 |

------

#### Q5：Object 类有哪些方法？

**equals：**检测对象是否相等，默认使用 `==` 比较对象引用，可以重写 equals 方法自定义比较规则。equals 方法规范：自反性、对称性、传递性、一致性、对于任何非空引用 x，`x.equals(null)` 返回 false。

**hashCode：**散列码是由对象导出的一个整型值，没有规律，每个对象都有默认散列码，值由对象存储地址得出。字符串散列码由内容导出，值可能相同。为了在集合中正确使用，一般需要同时重写 equals 和 hashCode，要求 equals 相同 hashCode 必须相同，hashCode 相同 equals 未必相同，因此 hashCode 是对象相等的必要不充分条件。

**toString**：打印对象时默认的方法，如果没有重写打印的是表示对象值的一个字符串。

**clone：**clone 方法声明为 protected，类只能通过该方法克隆它自己的对象，如果希望其他类也能调用该方法必须定义该方法为 public。如果一个对象的类没有实现 Cloneable 接口，该对象调用 clone 方***抛出一个 CloneNotSupport 异常。默认的 clone 方法是浅拷贝，一般重写 clone 方法需要实现 Cloneable 接口并指定访问修饰符为 public。

**finalize：**确定一个对象死亡至少要经过两次标记，如果对象在可达性分析后发现没有与 GC Roots 连接的引用链会被第一次标记，随后进行一次筛选，条件是对象是否有必要执行 finalize 方法。假如对象没有重写该方法或方法已被虚拟机调用，都视为没有必要执行。如果有必要执行，对象会被放置在 F-Queue 队列，由一条低调度优先级的 Finalizer 线程去执行。虚拟机会触发该方法但不保证会结束，这是为了防止某个对象的 finalize 方法执行缓慢或发生死循环。只要对象在 finalize 方法中重新与引用链上的对象建立关联就会在第二次标记时被移出回收集合。由于运行代价高昂且无法保证调用顺序，在 JDK 9 被标记为过时方法，并不适合释放资源。

**getClass：**返回包含对象信息的类对象。

**wait / notify / notifyAll：**阻塞或唤醒持有该对象锁的线程。

------

#### Q6：内部类的作用是什么，有哪些分类？

内部类可对同一包中其他类隐藏，内部类方法可以访问定义这个内部类的作用域中的数据，包括 private 数据。

内部类是一个编译器现象，与虚拟机无关。编译器会把内部类转换成常规的类文件，用 $ 分隔外部类名与内部类名，其中匿名内部类使用数字编号，虚拟机对此一无所知。

**静态内部类：** 属于外部类，只加载一次。作用域仅在包内，可通过 `外部类名.内部类名` 直接访问，类内只能访问外部类所有静态属性和方法。HashMap 的 Node 节点，ReentrantLock 中的 Sync 类，ArrayList 的 SubList 都是静态内部类。内部类中还可以定义内部类，如 ThreadLoacl 静态内部类 ThreadLoaclMap 中定义了内部类 Entry。

**成员内部类：** 属于外部类的每个对象，随对象一起加载。不可以定义静态成员和方法，可访问外部类的所有内容。

**局部内部类：** 定义在方法内，不能声明访问修饰符，只能定义实例成员变量和实例方法，作用范围仅在声明类的代码块中。

**匿名内部类：** 只用一次的没有名字的类，可以简化代码，创建的对象类型相当于 new 的类的子类类型。用于实现事件监听和其他回调。

------

#### Q7：访问权限控制符有哪些？

| 访问权限控制符 | 本类 | 包内 | 包外子类 | 任何地方 |
| -------------- | ---- | ---- | -------- | -------- |
| public         | √    | √    | √        | √        |
| protected      | √    | √    | √        | ×        |
| 无             | √    | √    | ×        | ×        |
| private        | √    | ×    | ×        | ×        |

------

#### Q8：接口和抽象类的异同？

接口和抽象类对实体类进行更高层次的抽象，仅定义公共行为和特征。

| 语法维度 | 抽象类                                             | 接口                                                         |
| -------- | -------------------------------------------------- | ------------------------------------------------------------ |
| 成员变量 | 无特殊要求                                         | 默认 public static final 常量                                |
| 构造方法 | 有构造方法，不能实例化                             | 没有构造方法，不能实例化                                     |
| 方法     | 抽象类可以没有抽象方法，但有抽象方法一定是抽象类。 | 默认 public abstract，JDK8 支持默认/静态方法，JDK9 支持私有方法。 |
| 继承     | 单继承                                             | 多继承                                                       |

------

#### Q9：接口和抽象类应该怎么选择？

抽象类体现 is-a 关系，接口体现 can-do 关系。与接口相比，抽象类通常是对同类事物相对具体的抽象。

抽象类是模板式设计，包含一组具体特征，例如某汽车，底盘、控制电路等是抽象出来的共同特征，但内饰、显示屏、座椅材质可以根据不同级别配置存在不同实现。

接口是契约式设计，是开放的，定义了方法名、参数、返回值、抛出的异常类型，谁都可以实现它，但必须遵守接口的约定。例如所有车辆都必须实现刹车这种强制规范。

接口是顶级类，抽象类在接口下面的第二层，对接口进行了组合，然后实现部分接口。当纠结定义接口和抽象类时，推荐定义为接口，遵循接口隔离原则，按维度划分成多个接口，再利用抽象类去实现这些，方便后续的扩展和重构。

例如 Plane 和 Bird 都有 fly 方法，应把 fly 定义为接口，而不是抽象类的抽象方法再继承，因为除了 fly 行为外 Plane 和 Bird 间很难再找到其他共同特征。

------

#### Q10：子类初始化的顺序

① 父类静态代码块和静态变量。② 子类静态代码块和静态变量。③ 父类普通代码块和普通变量。④ 父类构造方法。⑤ 子类普通代码块和普通变量。⑥ 子类构造方法。

------

### 集合 7

#### Q1：说一说 ArrayList

**ArrayList** 是容量可变的非线程安全列表，使用数组实现，集合扩容时会创建更大的数组，把原有数组复制到新数组。支持对元素的快速随机访问，但插入与删除速度很慢。ArrayList 实现了 RandomAcess 标记接口，如果一个类实现了该接口，那么表示使用索引遍历比迭代器更快。

**elementData**是 ArrayList 的数据域，被 transient 修饰，序列化时会调用 writeObject 写入流，反序列化时调用 readObject 重新赋值到新对象的 elementData。原因是 elementData 容量通常大于实际存储元素的数量，所以只需发送真正有实际值的数组元素。

**size** 是当前实际大小，elementData 大小大于等于 size。

**modCount **记录了 ArrayList 结构性变化的次数，继承自 AbstractList。所有涉及结构变化的方法都会增加该值。expectedModCount 是迭代器初始化时记录的 modCount 值，每次访问新元素时都会检查 modCount 和 expectedModCount 是否相等，不相等就会抛出异常。这种机制叫做 fail-fast，所有集合类都有这种机制。

------

#### Q2：说一说 LinkedList

**LinkedList** 本质是双向链表，与 ArrayList 相比插入和删除速度更快，但随机访问元素很慢。除继承 AbstractList 外还实现了 Deque 接口，这个接口具有队列和栈的性质。成员变量被 transient 修饰，原理和 ArrayList 类似。

LinkedList 包含三个重要的成员：size、first 和 last。size 是双向链表中节点的个数，first 和 last 分别指向首尾节点的引用。

LinkedList 的优点在于可以将零散的内存单元通过附加引用的方式关联起来，形成按链路顺序查找的线性结构，内存利用率较高。

------

#### Q3：Set 有什么特点，有哪些实现？

**Set** 不允许元素重复且无序，常用实现有 HashSet、LinkedHashSet 和 TreeSet。

**HashSet** 通过 HashMap 实现，HashMap 的 Key 即 HashSet 存储的元素，所有 Key 都使用相同的 Value ，一个名为 PRESENT 的 Object 类型常量。使用 Key 保证元素唯一性，但不保证有序性。由于 HashSet 是 HashMap 实现的，因此线程不安全。

HashSet 判断元素是否相同时，对于包装类型直接按值比较。对于引用类型先比较 hashCode 是否相同，不同则代表不是同一个对象，相同则继续比较 equals，都相同才是同一个对象。

**LinkedHashSet** 继承自 HashSet，通过 LinkedHashMap 实现，使用双向链表维护元素插入顺序。

**TreeSet** 通过 TreeMap 实现的，添加元素到集合时按照比较规则将其插入合适的位置，保证插入后的集合仍然有序。

------

#### Q4：TreeMap 有什么特点？

TreeMap 基于红黑树实现，增删改查的平均和最差时间复杂度均为 O(log~~n~~) ，最大特点是 Key 有序。Key 必须实现 Comparable 接口或提供的 Comparator 比较器，所以 Key 不允许为 null。

HashMap 依靠 `hashCode` 和 `equals` 去重，而 TreeMap 依靠 Comparable 或 Comparator。 TreeMap 排序时，如果比较器不为空就会优先使用比较器的 `compare` 方法，否则使用 Key 实现的 Comparable 的 `compareTo` 方法，两者都不满足会抛出异常。

TreeMap 通过 `put` 和 `deleteEntry` 实现增加和删除树节点。插入新节点的规则有三个：① 需要调整的新节点总是红色的。② 如果插入新节点的父节点是黑色的，不需要调整。③ 如果插入新节点的父节点是红色的，由于红黑树不能出现相邻红色，进入循环判断，通过重新着色或左右旋转来调整。TreeMap 的插入操作就是按照 Key 的对比往下遍历，大于节点值向右查找，小于向左查找，先按照二叉查找树的特性操作，后续会重新着色和旋转，保持红黑树的特性。

------

#### Q5：HashMap 有什么特点？

JDK8 之前底层实现是数组 + 链表，JDK8 改为数组 + 链表/红黑树，节点类型从Entry 变更为 Node。主要成员变量包括存储数据的 table 数组、元素数量 size、加载因子 loadFactor。

table 数组记录 HashMap 的数据，每个下标对应一条链表，所有哈希冲突的数据都会被存放到同一条链表，Node/Entry 节点包含四个成员变量：key、value、next 指针和 hash 值。

HashMap 中数据以键值对的形式存在，键对应的 hash 值用来计算数组下标，如果两个元素 key 的 hash 值一样，就会发生哈希冲突，被放到同一个链表上，为使查询效率尽可能高，键的 hash 值要尽可能分散。

HashMap 默认初始化容量为 16，扩容容量必须是 2 的幂次方、最大容量为 1<< 30 、默认加载因子为 0.75。

------

#### Q6：HashMap 相关方法的源码？

**JDK8 之前**

**hash：计算元素 key 的散列值**

① 处理 String 类型时，调用 `stringHash32` 方法获取 hash 值。

② 处理其他类型数据时，提供一个相对于 HashMap 实例唯一不变的随机值 hashSeed 作为计算初始量。

③ 执行异或和无符号右移使 hash 值更加离散，减小哈希冲突概率。

**indexFor：计算元素下标**

将 hash 值和数组长度-1 进行与操作，保证结果不会超过 table 数组范围。

**get：获取元素的 value 值**

① 如果 key 为 null，调用 `getForNullKey` 方法，如果 size 为 0 表示链表为空，返回 null。如果 size 不为 0 说明存在链表，遍历 table[0] 链表，如果找到了 key 为 null 的节点则返回其 value，否则返回 null。

② 如果 key 为 不为 null，调用 `getEntry` 方法，如果 size 为 0 表示链表为空，返回 null 值。如果 size 不为 0，首先计算 key 的 hash 值，然后遍历该链表的所有节点，如果节点的 key 和 hash 值都和要查找的元素相同则返回其 Entry 节点。

③ 如果找到了对应的 Entry 节点，调用 `getValue` 方法获取其 value 并返回，否则返回 null。

**put：添加元素**

① 如果 key 为 null，直接存入 table[0]。

② 如果 key 不为 null，计算 key 的 hash 值。

③ 调用 `indexFor` 计算元素存放的下标 i。

④ 遍历 table[i] 对应的链表，如果 key 已存在，就更新 value 然后返回旧 value。

⑤ 如果 key 不存在，将 modCount 值加 1，使用 `addEntry` 方法增加一个节点并返回 null。

**resize：扩容数组**

① 如果当前容量达到了最大容量，将阈值设置为 Integer 最大值，之后扩容不再触发。

② 否则计算新的容量，将阈值设为 `newCapacity x loadFactor` 和 `最大容量 + 1` 的较小值。

③ 创建一个容量为 newCapacity 的 Entry 数组，调用 `transfer` 方法将旧数组的元素转移到新数组。

**transfer：转移元素**

① 遍历旧数组的所有元素，调用 `rehash` 方法判断是否需要哈希重构，如果需要就重新计算元素 key 的 hash 值。

② 调用 `indexFor` 方法计算元素存放的下标 i，利用头插法将旧数组的元素转移到新数组。

**JDK8**

**hash：计算元素 key 的散列值**

如果 key 为 null 返回 0，否则就将 key 的 `hashCode` 方法返回值高低16位异或，让尽可能多的位参与运算，让结果的 0 和 1 分布更加均匀，降低哈希冲突概率。

**put：添加元素**

① 调用 `putVal` 方法添加元素。

② 如果 table 为空或长度为 0 就进行扩容，否则计算元素下标位置，不存在就调用 `newNode` 创建一个节点。

③ 如果存在且是链表，如果首节点和待插入元素的 hash 和 key 都一样，更新节点的 value。

④ 如果首节点是 TreeNode 类型，调用 `putTreeVal` 方法增加一个树节点，每一次都比较插入节点和当前节点的大小，待插入节点小就往左子树查找，否则往右子树查找，找到空位后执行两个方法：`balanceInsert` 方法，插入节点并调整平衡、`moveRootToFront` 方法，由于调整平衡后根节点可能变化，需要重置根节点。

⑤ 如果都不满足，遍历链表，根据 hash 和 key 判断是否重复，决定更新 value 还是新增节点。如果遍历到了链表末尾则添加节点，如果达到建树阈值 7，还需要调用 `treeifyBin` 把链表重构为红黑树。

⑥ 存放元素后将 modCount 加 1，如果 `++size > threshold` ，调用 `resize` 扩容。

**get ：获取元素的 value 值**

① 调用 `getNode` 方法获取 Node 节点，如果不是 null 就返回其 value 值，否则返回 null。

② `getNode` 方法中如果数组不为空且存在元素，先比较第一个节点和要查找元素的 hash 和 key ，如果都相同则直接返回。

③ 如果第二个节点是 TreeNode 类型则调用 `getTreeNode` 方法进行查找，否则遍历链表根据 hash 和 key 查找，如果没有找到就返回 null。

**resize：扩容数组**

重新规划长度和阈值，如果长度发生了变化，部分数据节点也要重新排列。

**重新规划长度**

① 如果当前容量 `oldCap > 0` 且达到最大容量，将阈值设为 Integer 最大值，return 终止扩容。

② 如果未达到最大容量，当 `oldCap << 1` 不超过最大容量就扩大为 2 倍。

③ 如果都不满足且当前扩容阈值 `oldThr > 0`，使用当前扩容阈值作为新容量。

④ 否则将新容量置为默认初始容量 16，新扩容阈值置为 12。

**重新排列数据节点**

① 如果节点为 null 不进行处理。

② 如果节点不为 null 且没有next节点，那么通过节点的 hash 值和 `新容量-1` 进行与运算计算下标存入新的 table 数组。

③ 如果节点为 TreeNode 类型，调用 `split` 方法处理，如果节点数 hc 达到6 会调用 `untreeify` 方法转回链表。

④ 如果是链表节点，需要将链表拆分为 hash 值超出旧容量的链表和未超出容量的链表。对于`hash & oldCap == 0` 的部分不需要做处理，否则需要放到新的下标位置上，新下标 = 旧下标 + 旧容量。

------

#### Q7：HashMap 为什么线程不安全？

JDK7 存在死循环和数据丢失问题。

**数据丢失：**

- **并发赋值被覆盖：** 在 `createEntry` 方法中，新添加的元素直接放在头部，使元素之后可以被更快访问，但如果两个线程同时执行到此处，会导致其中一个线程的赋值被覆盖。
- **已遍历区间新增元素丢失：** 当某个线程在 `transfer` 方法迁移时，其他线程新增的元素可能落在已遍历过的哈希槽上。遍历完成后，table 数组引用指向了 newTable，新增元素丢失。
- **新表被覆盖：** 如果 `resize` 完成，执行了 `table = newTable`，则后续元素就可以在新表上进行插入。但如果多线程同时 `resize` ，每个线程都会 new 一个数组，这是线程内的局部对象，线程之间不可见。迁移完成后`resize` 的线程会赋值给 table 线程共享变量，可能会覆盖其他线程的操作，在新表中插入的对象都会被丢弃。

**死循环：** 扩容时 `resize` 调用 `transfer` 使用头插法迁移元素，虽然 newTable 是局部变量，但原先 table 中的 Entry 链表是共享的，问题根源是 Entry 的 next 指针并发修改，某线程还没有将 table 设为 newTable 时用完了 CPU 时间片，导致数据丢失或死循环。

JDK8 在 `resize` 方法中完成扩容，并改用尾插法，不会产生死循环，但并发下仍可能丢失数据。可用 ConcurrentHashMap 或 `Collections.synchronizedMap` 包装成同步集合。

------

### IO 流 6

#### Q1：同步/异步/阻塞/非阻塞 IO 的区别？

同步和异步是通信机制，阻塞和非阻塞是调用状态。

同步 IO 是用户线程发起 IO 请求后需要等待或轮询内核 IO 操作完成后才能继续执行。异步 IO 是用户线程发起 IO 请求后可以继续执行，当内核 IO 操作完成后会通知用户线程，或调用用户线程注册的回调函数。

阻塞 IO 是 IO 操作需要彻底完成后才能返回用户空间 。非阻塞 IO 是 IO 操作调用后立即返回一个状态值，无需等 IO 操作彻底完成。

------

#### Q2：什么是 BIO？

**BIO** 是同步阻塞式 IO，JDK1.4 之前的 IO 模型。服务器实现模式为一个连接请求对应一个线程，服务器需要为每一个客户端请求创建一个线程，如果这个连接不做任何事会造成不必要的线程开销。可以通过线程池改善，这种 IO 称为伪异步 IO。适用连接数目少且服务器资源多的场景。

------

#### Q3：什么是 NIO？

**NIO** 是 JDK1.4 引入的同步非阻塞 IO。服务器实现模式为多个连接请求对应一个线程，客户端连接请求会注册到一个多路复用器 Selector ，Selector 轮询到连接有 IO 请求时才启动一个线程处理。适用连接数目多且连接时间短的场景。

同步是指线程还是要不断接收客户端连接并处理数据，非阻塞是指如果一个管道没有数据，不需要等待，可以轮询下一个管道。

核心组件：

- **Selector：** 多路复用器，轮询检查多个 Channel 的状态，判断注册事件是否发生，即判断 Channel 是否处于可读或可写状态。使用前需要将 Channel 注册到 Selector，注册后会得到一个 SelectionKey，通过 SelectionKey 获取 Channel 和 Selector 相关信息。

- **Channel：** 双向通道，替换了 BIO 中的 Stream 流，不能直接访问数据，要通过 Buffer 来读写数据，也可以和其他 Channel 交互。

- **Buffer：** 缓冲区，本质是一块可读写数据的内存，用来简化数据读写。Buffer 三个重要属性：position 下次读写数据的位置，limit 本次读写的极限位置，capacity 最大容量。

  - `flip` 将写转为读，底层实现原理把 position 置 0，并把 limit 设为当前的 position 值。 
  - `clear` 将读转为写模式（用于读完全部数据的情况，把 position 置 0，limit 设为 capacity）。 
  - `compact` 将读转为写模式（用于存在未读数据的情况，让 position 指向未读数据的下一个）。 
  - 通道方向和 Buffer 方向相反，读数据相当于向 Buffer 写，写数据相当于从 Buffer 读。 

  使用步骤：向 Buffer 写数据，调用 flip 方法转为读模式，从 Buffer 中读数据，调用 clear 或 compact 方法清空缓冲区。

------

#### Q4：什么是 AIO？

AIO 是 JDK7 引入的异步非阻塞 IO。服务器实现模式为一个有效请求对应一个线程，客户端的 IO 请求都是由操作系统先完成 IO 操作后再通知服务器应用来直接使用准备好的数据。适用连接数目多且连接时间长的场景。

异步是指服务端线程接收到客户端管道后就交给底层处理IO通信，自己可以做其他事情，非阻塞是指客户端有数据才会处理，处理好再通知服务器。

实现方式包括通过 Future 的 `get` 方法进行阻塞式调用以及实现 CompletionHandler 接口，重写请求成功的回调方法 `completed` 和请求失败回调方法 `failed`。

------

#### Q5：java.io 包下有哪些流？

主要分为字符流和字节流，字符流一般用于文本文件，字节流一般用于图像或其他文件。

字符流包括了字符输入流 Reader 和字符输出流 Writer，字节流包括了字节输入流 InputStream 和字节输出流 OutputStream。字符流和字节流都有对应的缓冲流，字节流也可以包装为字符流，缓冲流带有一个 8KB 的缓冲数组，可以提高流的读写效率。除了缓冲流外还有过滤流 FilterReader、字符数组流 CharArrayReader、字节数组流 ByteArrayInputStream、文件流 FileInputStream 等。

------

#### Q6：序列化和反序列化是什么？

Java 对象 JVM 退出时会全部销毁，如果需要将对象及状态持久化，就要通过序列化实现，将内存中的对象保存在二进制流中，需要时再将二进制流反序列化为对象。对象序列化保存的是对象的状态，因此属于类属性的静态变量不会被序列化。

常见的序列化有三种：

- **Java 原生序列化**

  实现 `Serializabale` 标记接口，Java 序列化保留了对象类的元数据（如类、成员变量、继承类信息）以及对象数据，兼容性最好，但不支持跨语言，性能一般。序列化和反序列化必须保持序列化 ID 的一致，一般使用 `private static final long serialVersionUID` 定义序列化 ID，如果不设置编译器会根据类的内部实现自动生成该值。如果是兼容升级不应该修改序列化 ID，防止出错，如果是不兼容升级则需要修改。

- **Hessian 序列化**

  Hessian 序列化是一种支持动态类型、跨语言、基于对象传输的网络协议。Java 对象序列化的二进制流可以被其它语言反序列化。Hessian 协议的特性：① 自描述序列化类型，不依赖外部描述文件，用一个字节表示常用基础类型，极大缩短二进制流。② 语言无关，支持脚本语言。③ 协议简单，比 Java 原生序列化高效。Hessian 会把复杂对象所有属性存储在一个 Map 中序列化，当父类和子类存在同名成员变量时会先序列化子类再序列化父类，因此子类值会被父类覆盖。

- **JSON 序列化**

  JSON 序列化就是将数据对象转换为 JSON 字符串，在序列化过程中抛弃了类型信息，所以反序列化时只有提供类型信息才能准确进行。相比前两种方式可读性更好，方便调试。

序列化通常会使用网络传输对象，而对象中往往有敏感数据，容易遭受攻击，Jackson 和 fastjson 等都出现过反序列化漏洞，因此不需要进行序列化的敏感属性传输时应加上 transient 关键字。transient 的作用就是把变量生命周期仅限于内存而不会写到磁盘里持久化，变量会被设为对应数据类型的零值。