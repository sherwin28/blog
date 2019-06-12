---
title: String的split小记
date: 2018-03-30 17:35:41
tags: java基础
categories: java
---

```
    public class SplitDemo {
        public static void main(String[] args) {
            String a = "abcooob";
            String[] as = a.split("o");
            System.out.println(as.length);
        }
    }
```
运行结果是

4
abc            b

因为分割成{“abc”,"","","b"}的值，这个正常理解。

```
    public class SplitDemo {
        public static void main(String[] args) {
            String a = "abcooo";
            String[] as = a.split("o");
            System.out.println(as.length);
            for (String string : as) {
                System.out.print(string+"\t");
            }
        }
    }
```
这个运行结果是：

1
abc
---------------------------------------------------------

为什么呢？

看api

![image](http://p5zbw6dku.bkt.clouddn.com/18-3-30/88195363.jpg)



split
public String[] split(String regex)
根据给定正则表达式的匹配拆分此字符串。

该方法的作用就像是使用给定的表达式和限制参数 0 来调用两参数 split 方法。因此，所得数组中不包括结尾空字符串。

例如，字符串 "boo:and:foo" 使用这些表达式可生成以下结果：

Regex	结果
:	{ "boo", "and", "foo" }
o	{ "b", "", ":and:f" }


参数：

regex - 定界正则表达式

返回：

字符串数组，它是根据给定正则表达式的匹配拆分此字符串确定的

抛出：

PatternSyntaxException - 如果正则表达式的语法无效





----------------------------------------------------------------------------------

结论：split分割所得数组中不包括结尾空字符串。

----------------------------------------------------------------------------------