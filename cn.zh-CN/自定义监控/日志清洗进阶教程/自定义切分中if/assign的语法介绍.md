# 自定义切分中if/assign的语法介绍

ARMS默认支持Aviator表达式引擎，您可以完成对数据处理时的逻辑控制、赋值操作等。

## 条件判断if-else

在自定义切分标签页的左侧操作面板中选择**逻辑**，系统提供两种类型的逻辑判断积木块“if/else”和“if”，如下图所示。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7729339851/p44128.png)

下图演示一些简单的逻辑表达式使用例子，用户日志如下所示。

```
2017-01-09 16:02:49|ERROR|it is error...
2017-01-09 16:03:49|INFO|it is ok...
2017-01-09 16:03:49|INFO_1|it is ok...
```

日志按照“\|”切分之后的字段分别为`date`、`type`、`message`。

示例一：当`type`为INFO时，该行日志直接丢弃。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8729339851/p44129.png)

示例二：当`type`包含INFO的时候，该行日志丢弃。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8729339851/p44130.png)

## 赋值

接下来演示一个简单的赋值使用例子，用户日志如下所示。

```
2017-01-09 16:02:49|松江区2017-01-09 16:03:49|浦东区2017-01-09 16:03:49|上城区2017-01-09 16:03:49|下城区
```

日志按照“\|”切分之后的字段分别为`date`、`region`。如果`region`为“松江区”或者“浦东区”，则添加一个新的字段`province`（String类型），其值为“上海市”；如果`region`为“上城区”或者“下城区”，则添加一个新的字段`province`（String类型），其值为“杭州市”。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8729339851/p44131.png)

## 内置函数（转自Aviator官方文档）

Aviator表达式是一个开源产品（[点此查看官方文档](https://code.google.com/archive/p/aviator/wikis/User_Guide_zh.wiki)）。常见内置函数的说明如下表所示。

|函数|描述|
|--|--|
|sysdate\(\)|返回当前日期对象java.util.Date|
|rand\(\)|返回一个介于0~1的Double类型的随机数|
|now\(\)|返回System.currentTimeMillis|
|long\(v\)|将值的类型转为Long|
|double\(v\)|将值的类型转为Double|
|date\_to\_string\(date,format\)|将Date对象转化为特定格式的字符串|
|string\_to\_date\(source,format\)|将特定格式的字符串转化为Date对象|
|string.contains\(s1,s2\)|判断s1是否包含s2，返回Boolean类型的值。|
|string.length\(s\)|求字符串长度，返回Long类型的值。|
|string.startsWith\(s1,s2\)|s1是否以s2开始，返回Boolean类型的值。|
|string.endsWith\(s1,s2\)|s1是否以s2结尾，返回Boolean类型的值。|
|string.substring\(s,begin\[,end\]\)|截取字符串s，从begin到end，end如果忽略的话，将从begin到结尾，与java.util.String.substring一样。|
|string.indexOf\(s1,s2\)|Java中的s1.indexOf\(s2\)，求s2在s1中的起始索引位置，如果不存在则为-1。|
|string.split\(target,regex,\[limit\]\)|Java里的String.split方法一致|
|string.replace\_first\(s,regex,replacement\)|Java里的String.replaceFirst方法|
|string.replace\_all\(s,regex,replacement\)|Java里的String.replaceAll方法|
|math.abs\(d\)|求d的绝对值|
|math.sqrt\(d\)|求d的平方根|
|math.pow\(d1,d2\)|求d1的d2次方|
|math.log\(d\)|求d的自然对数|
|math.log10\(d\)|求d以10为底的对数|
|math.sin\(d\)|正弦函数|
|math.cos\(d\)|余弦函数|
|math.tan\(d\)|正切函数|

