---
title: mybatis3 中provider的使用
date: 2018-03-15 17:35:41
tags: mybatis
categories: mybatis
---

 mybatis3提供了4个**provider注解，分别对应增删改查，分别是:InsertProvider、DeleteProvider、UpdateProvider、SelectProvider;如何使用这些注解呢？

1.这些注解都有统一的2个入参，一个是type，一个是method。type参数的值是你动态sql的类（A）class文件，method是类（A）中的方法名。当然，这些方法都是动态sql，至于动态sql怎么实现，这就可以发挥你的java基础能力，我是结合了自定义注解和java反射基础知识实现了动态sql。下面结合代码讲解一下实现过程。

2.首先你需要定义一个接口类，这个类提供各种各样的增删改查方法。

下面以@SelectProvider为例，依次描述几种典型的使用场景。

1.使用@SelectProvider
@SelectProvider是声明在方法基本上的，这个方法定义在Mapper对应的的interface上。

```java
public interface UserMapper {
     @SelectProvider(type = SqlProvider.class, method = "selectUser")
     @ResultMap("userMap")
     public User getUser(long userId);
}
```

上例中是个很简单的Mapper接口，其中定义了一个方法：getUser，这个方法根据提供的用户id来查询用户信息，并返回一个User实体bean。
这是一个很简单很常用的查询场景：根据key来查询记录并将结果封装成实体bean。其中：
@SelectProvider注解用于生成查询用的sql语句，有别于@Select注解，@SelectProvide指定一个Class及其方法，并且通过调用Class上的这个方法来获得sql语句。在我们这个例子中，获取查询sql的方法是SqlProvider.selectUser。
@ResultMap注解用于从查询结果集RecordSet中取数据然后拼装实体bean。
 
2.定义拼装sql的类
@SelectProvide中type参数指定的Class类，必须要能够通过无参的构造函数来初始化。
@SelectProvide中method参数指定的方法，必须是public的，返回值必须为String，可以为static。
```java
public class SqlProvider {
    public String selectUser(long userId) {
        return "select * from user where userId=" + userId;
    }
}
```
上面的就是个简单使用，就可以在mybatis中拼接sql了，有这个之后就可以改造mybatis用实体来查询了，就像hibernate一样了。

附加几个mybatis中不常用但很有意思的OGNL用法。
* e.method(args) : 调用对象的方法
* e.property： 对象属性值，可以多层嵌套使用，
* e1[e2] :按索引取值（list，数组和map，map使用的时候注意key一样的存在，不存在会报错的）
* @class@method(args):调用类的静态方法
* @class@field:调用类的静态字段值

