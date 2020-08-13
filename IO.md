## BufferedReader

庆哥：这个BufferedReader我们可以好好说一下，因为这个在平常使用的挺多的，相信你应该也有印象，我们使用BufferedReader读取文本内容可以保证文本内容的格式不被打乱，反正吧，关于BufferedReader的用法一定要熟练，BufferedReader我们叫做缓冲流，当然是对Reader做缓冲的，所以使用BufferedReader一定会用到Reader，接下来我们看看代码就知道了

```java
//法1
//使用InputStreamReader
FileInputStream fileInputStream = new FileInputStream(file);
//获取字符输入流
InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream);
BufferedReader bufferedReader = new BufferedReader(inputStreamReader);

//法2
BufferedReader br = new BufferedReader(new FileReader(file));

String line = null;
while ((line=bufferedReader.readLine())!= null){
  System.out.println(line);
}

```

这段代码一定要记住了，烂熟于心，我们看代码知道这个BufferedReader需要接收一个字符流 InputStreamReader，然后就可以直接调取readLine方法进行整行读取，会得到一个字符串，可以直接输出，因为是整行读取可以保持格式不乱，真的很好用，所以要记住了
————————————————
版权声明：本文为CSDN博主「ithuangqing」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/sinat_33921105/article/details/81081452



## 序列化与反序列化

### 一、序列化的含义、意义及使用场景

- **序列化：将对象写入到IO流中**
- **反序列化：从IO流中恢复对象**
- **意义：序列化机制允许将实现序列化的Java对象转换位字节序列，这些字节序列可以保存在磁盘上，或通过网络传输，以达到以后恢复成原来的对象。序列化机制使得对象可以脱离程序的运行而独立存在。**
- **使用场景：所有可在网络上传输的对象都必须是可序列化的，**比如RMI（remote method invoke,即远程方法调用），传入的参数或返回的对象都是可序列化的，否则会出错；**所有需要保存到磁盘的java对象都必须是可序列化的。通常建议：程序创建的每个JavaBean类都实现Serializeable接口。**

### 二、序列化实现的方式

如果需要将某个对象保存到磁盘上或者通过网络传输，那么这个类应该实现**Serializable**接口或者**Externalizable**接口之一。

#### 1、Serializable

##### 1.1 普通序列化

Serializable接口是一个标记接口，不用实现任何方法。一旦实现了此接口，该类的对象就是可序列化的。

1. **序列化步骤：**
   - 步骤一：创建一个ObjectOutputStream输出流；
   - 步骤二：调用ObjectOutputStream对象的writeObject输出可序列化对象。
2. **反序列化步骤：**
   - 步骤一：创建一个ObjectInputStream输入流；
   - 步骤二：调用ObjectInputStream对象的readObject()得到序列化的对象。

#### 2、Externalizable：强制自定义序列化

通过实现Externalizable接口，必须实现writeExternal、readExternal方法。

**Externalizable接口不同于Serializable接口，实现此接口必须实现接口中的两个方法实现自定义序列化，这是强制性的；特别之处是必须提供pulic的无参构造器，因为在反序列化的时候需要反射创建对象。**



- **Java序列化算法**

1. **所有保存到磁盘的对象都有一个序列化编码号**
2. **当程序试图序列化一个对象时，会先检查此对象是否已经序列化过，只有此对象从未（在此虚拟机）被序列化过，才会将此对象序列化为字节序列输出。**
3. **如果此对象已经序列化过，则直接输出编号即可。**



**总结**

1. 所有需要网络传输的对象都需要实现序列化接口，通过建议所有的javaBean都实现Serializable接口。
2. 对象的类名、实例变量（包括基本类型，数组，对其他对象的引用）都会被序列化；方法、类变量、transient实例变量都不会被序列化。
3. 如果想让某个变量不被序列化，使用transient修饰。
4. 序列化对象的引用类型成员变量，也必须是可序列化的，否则，会报错。
5. 反序列化时必须有序列化对象的class文件。
6. 当通过文件、网络来读取序列化后的对象时，必须按照实际写入的顺序读取。
7. 单例类序列化，需要重写readResolve()方法；否则会破坏单例原则。
8. 同一对象序列化多次，只有第一次序列化为二进制流，以后都只是保存序列化编号，不会重复序列化。
9. 建议所有可序列化的类加上serialVersionUID 版本号，方便项目升级。

https://www.cnblogs.com/9dragon/p/10901448.html



## [IO、NIO、AIO详解](https://www.cnblogs.com/sxkgeek/p/9488703.html)

- 同步与异步（synchronous/asynchronous）：**同步**是一种可靠的有序运行机制，当我们进行同步操作时，后续的任务是等待当前调用返回，才会进行下一步；而**异步**则相反，其他任务不需要等待当前调用返回，通常依靠事件、回调等机制来实现任务间次序关系
- 阻塞与非阻塞：在进行**阻塞**操作时，当前线程会处于阻塞状态，无法从事其他任务，只有当条件就绪才能继续，比如ServerSocket新连接建立完毕，或者数据读取、写入操作完成；而**非阻塞**则是不管IO操作是否结束，直接返回，相应操作在后台继续处理

- [一、IO流（同步、阻塞）](https://www.cnblogs.com/sxkgeek/p/9488703.html#_label1)（BIO）
- [二、NIO（同步、非阻塞）](https://www.cnblogs.com/sxkgeek/p/9488703.html#_label2)
- [三、NIO2(异步、非阻塞)](https://www.cnblogs.com/sxkgeek/p/9488703.html#_label3)（AIO）

```
NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持。
AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持
```

