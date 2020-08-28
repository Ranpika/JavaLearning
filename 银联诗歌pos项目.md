参与项目介绍：
云闪付app中的公益小程序，内容是用户参与助力，帮助贫困山区的孩子们建造图书馆，用户每天有一定的助力次数限制，每次参与助力后台会返回一首孩子写的诗歌，用户个人页面能看到获得的诗歌、助力次数、项目反馈，项目助力额度满后结束；
技术上使用SSM框架，使用Redis缓存，使用MySql数据库，通过Mybatis Plus完成与数据库交互； 

职责：

1 完成助力相关接口的开发工作，并用postman进行接口测试；

2 完成MySql数据库分表工作，制定不同的分表策略；

3 实现用traceId追踪不同线程的日志，从而更方便地查看日志；

4 与测试同事进行沟通，查找错误，调整需求，修改接口代码；

5 实现数据库与Redis的事务，保障数据操作的安全性；

5 实现项目最新反馈信息的用户推送，并在小程序中用小红点标注，使用线程池技术，并异步调用。

## 框架

ssm+redis+mysql

## 实现

### 1 分页

mybatis plus 配置 分页拦截器

![image-20200727165005274](/Users/ran/Library/Application Support/typora-user-images/image-20200727165005274.png)

service中进行查找

![image-20200727165048468](/Users/ran/Library/Application Support/typora-user-images/image-20200727165048468.png)

#### 问题

不能成功将git下来的项目解析为maven项目

##### 后台得不到前端传入的参数，传入为null

Controller

![image-20200727151739518](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200727151739518.png?lastModify=1596768528)

postman

![image-20200727154134585](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200727154134585.png?lastModify=1596768528)

原因：

注解错误，不能用@RequestParam (这个注解对应的是url里 ?openId=001)

![image-20200728100814383](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200728100814383.png?lastModify=1596768528)

应该用@RequestBody

Map<String,Object>形式传入json格式数据

![image-20200728103614164](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200728103614164.png?lastModify=1596768528)

![image-20200728103647862](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200728103647862.png?lastModify=1596768528)



自测：postman

![image-20200728105722899](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200728105722899.png?lastModify=1596768528)

![image-20200728105754558](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200728105754558.png?lastModify=1596768528)

![image-20200729142625656](file:///Users/ran/Library/Application%20Support/typora-user-images/image-20200729142625656.png?lastModify=1596768528)

需要设置produces才能让返回值为json格式，不然会报错

### 2 异步日志

使用@Slf4j打印log4j2日志

1 使用MDC实现TraceId追踪（增加拦截器）

​	原理：threadLocal 每个线程一个

2 pom配置

### 3 数据库分表

sharding实现

1 Application.yml进行配置，给出分表策略；

​	   分表策略：使用openid划分，字符串获取hashcode，再对表的数量取余

​					对于donate_log表，用日期分表，便于查看log记录，设置1-31张表，对应各个日期

2 数据库里手动添加表

3 加入分表拦截器SharingConfig

4 pom配置

![image-20200811195954846](/Users/ran/Library/Application Support/typora-user-images/image-20200811195954846.png)

![image-20200811195702307](/Users/ran/Library/Application Support/typora-user-images/image-20200811195702307.png)

#### 问题

openId字符串比较长，获取的hashcode是负数，使得分片为负数，找不到对应的分片。

String 生成hashCode的代码：

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```java
 /**
     * Returns a hash code for this string. The hash code for a
     * {@code String} object is computed as
     * <blockquote><pre>
     * s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]
     * </pre></blockquote>
     * using {@code int} arithmetic, where {@code s[i]} is the
     * <i>i</i>th character of the string, {@code n} is the length of
     * the string, and {@code ^} indicates exponentiation.
     * (The hash value of the empty string is zero.)
     *
     * @return  a hash code value for this object.
     */
    public int hashCode() {
        int h = hash;
        if (h == 0 && value.length > 0) {
            char val[] = value;

            for (int i = 0; i < value.length; i++) {
                h = 31 * h + val[i];
            }
            hash = h;
        }
        return h;
    }
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

主要是根据字符串中字符的ascii码值来计算的，即 31 * hash + 字符的ASCII码值，int型的值取值范围为Integer.MIN_VALUE(-2147483648)～Integer.MAX_VALUE(2147483647)，所以如果字符串比较长，计算的数值就可能超出Integer.MAX_VALUE，造成数值溢出，值变成负数。

解决办法：

要想利用hashCode为非负数，可以Integer.MAX_VALUE和与操作，这样最大正整数的符号位为0，与任何数与操作都是0，即是正数

```
int hash = str.hashCode() & Integer.MAX_VALUE;
```

 2 分表拦截器中，传入参数类型为TimeStamp类型（数据库中的），会报错

解决方法：转成date类型

![image-20200811195930333](/Users/ran/Library/Application Support/typora-user-images/image-20200811195930333.png)

### 4 springboot事务

在需要插入数据库的方法上面 用 @Transactional注解

验证：在方法返回前写一个unchecked exception，（int a = 10/0;) 看错误发生前对数据库的操作是否成功了。

### 5 Redis事务

redisUpdateUtil里：

![3671597198008_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3671597198008_.pic_hd.jpg)

UserController里：

![3681597198009_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3681597198009_.pic_hd.jpg)

![3691597198010_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3691597198010_.pic_hd.jpg)![3701597198011_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3701597198011_.pic_hd.jpg)

![3711597198012_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3711597198012_.pic_hd.jpg)

![3721597198013_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3721597198013_.pic_hd.jpg)

![3731597198014_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3731597198014_.pic_hd.jpg)

redisUpdateUtil里：

![3741597198015_.pic_hd](/Users/ran/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/e65916c870f7e965491f95121e76d711/Message/MessageTemp/9e20f478899dc29eb19741386f9343c8/Image/3741597198015_.pic_hd.jpg)

实现redis事务，给一个标记ops=1，如果需要更新redis的地方，把ops|一个固定的数（该数为2倍数，二进制里只有一位为1），在return前统一进行redis的更新，判断不同的key是否需要更新，判断方法为将ops&不同key的固定数，如果结果不为0，则需要更新这个key对应的值

### 6 反馈推送

实现项目最新反馈信息的用户推送，并在小程序中用小红点标注，使用线程池技术，并异步调用方法

第一步：push方法

controller中：

![image-20200819191259696](/Users/ran/Library/Application Support/typora-user-images/image-20200819191259696.png)

openPlatformUtil中：

![image-20200819191320998](/Users/ran/Library/Application Support/typora-user-images/image-20200819191320998.png)

HttpClientUtil中：

![image-20200819191408706](/Users/ran/Library/Application Support/typora-user-images/image-20200819191408706.png)

第二步：给所有用户推送，并异步调用

![image-20200819191453059](/Users/ran/Library/Application Support/typora-user-images/image-20200819191453059.png)

<img src="/Users/ran/Library/Application Support/typora-user-images/image-20200819191511446.png" alt="image-20200819191511446" style="zoom:50%;" />

PushSup中（Service层）：

![image-20200819191934379](/Users/ran/Library/Application Support/typora-user-images/image-20200819191934379.png)

![image-20200819192004208](/Users/ran/Library/Application Support/typora-user-images/image-20200819192004208.png)

线程池配置，AsyncConfig中：

![image-20200819192020248](/Users/ran/Library/Application Support/typora-user-images/image-20200819192020248.png)

![image-20200819192103860](/Users/ran/Library/Application Support/typora-user-images/image-20200819192103860.png)

spring的一个异步注解@Async -- 实现异步调用

 不再新建线程类了，这个过程交给spring线程池去处理

参考：https://blog.csdn.net/lw1124052197/article/details/81980272?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase

## 部署遇到问题

404bad request

![image-20200811200035718](/Users/ran/Library/Application Support/typora-user-images/image-20200811200035718.png)

400错 bad request 由于明显的客户端错误（例如，格式错误的请求语法，太大的大小，无效的请求消息或欺骗性路由请求），服务器不能或不会处理该请求。

## 数据库遇到问题

遇到问题：数据库中的某张表中的数据会发生丢失，每次只丢失一条，每天只丢失一两次

看日志记录，没有问题，不是误删，只发现在需要更新userdonateinformation表时（当用户点击助力诗歌，返回了一首用户助力过的诗歌，会更新这个诗歌的助力次数），会将表中所有数据都进行更新，找不到问题，怀疑数据库被人修改。

发现疑点：如果从数据库中手动删除一条记录，自增列id不会改变，会在中间缺失一个id，但是每次遇到数据库中数据丢失问题时，自增列id是有序的

原因：表是按照openid进行分表的，而update是原来写的方法，是按照id进行update，每次update时无法根据id在各个分表之中进行搜索，而会比较智能地update所有的数据，并找到搜索id所对应的数据行，更改那行数据为需要更新的数据，因此原本那行所拥有的用户信息就丢失了

解决方案：重新写update方法，根据openId进行更新

