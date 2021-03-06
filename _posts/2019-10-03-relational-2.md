---
title: 五十年前的一桩公案：数据库关系模型的流行史（下）
---

如果说[上篇]({% post_url 2019-10-02-relational-1 %})讲的是关系模型今天的样子的话，这篇关注的就是它被科德提出时本来的样子。

不管什么时候，关系模型本质上的优点都是成立的，一是更独立更强大的表达能力，二是只管表达结果不管实现过程，两者相辅相成。

既然说表达与实现相分离，那我们就从这两方面分别来说一说。

先说表达。

关系模型简洁、强大，几乎无懈可击。但它在刚提出的时候，因为用的是集合论的语言，被批评为“太数学”，不易于程序员理解。

在今天，很多人最初接触关系模型并不是通过集合论，而是通过SQL，好像并没有太大理解上的问题。

是因为SQL的表达更简单吗？

以前我以为，SQL在保证语言完备的情况下，简化了科德最初的模型，妥协了表达的效率。这次读了原文，发现它其实和SQL一样简单，几乎一一对应。

所以与其说关系模型难以理解，不如说它一时间不被接受。就好比在广义相对论提出时，物理学者可能会觉得非欧几何“太数学”，而现在却成为他们的基础知识。



再说实现。

我们今天可能会觉得关系模型简直是数据一致性（consistency）的福音。

因为关系本身没有重复的信息，数据不一致的情况只可能出现在由其衍生出的数据上，如索引（index）和物化视图（materialized view）。这些衍生数据并没有新的信息，只是用来提高计算效率。

在现代的数据库中，它们的一致性是由数据库系统来维护的。数据库会在用户增删改原始数据的同时，相应修改衍生数据。因而数据库的应用者根本不用担心。

但科德最初并不是这么想的。在他的意识中，输入这些衍生数据、并确保它们一致，还属于用户自己的责任。

他对此感到忧虑，并提出了两种解决办法。一种是用户增删改数据后，系统在后台检查一致性，当发现问题时拉响警报。另一种是每过几天，系统全盘检查一遍，看看是不是有一致性的问题。

这在今天的我们看来，不亚于那个苏联冷笑话：

> 美国外交代表团到苏联访问，苏修接待官员陪他们参观建设的伟大成就，并且得意的说：到了下一个五年计划，每个苏联家庭都可以拥有一架私人飞机！
>
> 美国人惊讶的问：他们要飞机干什么呢？
>
> 苏修官员说：当然有用啊……譬如你在莫斯科听说列宁格勒开始供应面包了，你可以马上开飞机赶去排队啊。

现在，我们可以讲五十年前发生了什么了。

与科德同时，还有一伙人也看到了层次模型的弱点，提出了网状模型。

层次模型本质上是一棵树，所以难以解决数据间错综复杂的依赖关系。既然树的表达能力不行，改用网络表达水到渠成。

具体网状模型的思想限于篇幅不介绍了，读者可以根据层次模型来想象猜测一下。如果用一句话就是，它跟关系模型挺像的。

但就跟任何其它宗教一样，越接近，越有斗争。

以科德为代表的“关系派”与以巴赫曼（Charles Bachman）为代表的“网状派”针锋相对，在七十年代引发数次大讨论。

“关系派”的一大罪状，如前面所说，是科德提出的关系模型“晦涩难懂”。但他们很快就设计了SQL等专用于数据库操作的语言，老幼皆宜。

“关系派”还被怀疑难以得到高性能的实现，因为这个模型太理想化了。按照我们前面的观察，它起初确实是这样。但短短几年里一系列理论和算法的提出让它迅速充实起来，之后关系型数据库System R的问世更是打消了人们的这一顾虑。



“网状派”也有槽点。他们使用的语言是需要描述过程的，对提高生产力很不友好。但后来他们也提出了一种像SQL一样描述结果的语言。

在相互借鉴和发展中，其实两个模型都实现了各自的设计目标，也都渐渐弥补了各自的不足，甚至变得越来越接近。（老对头科德和巴赫曼后来都拿到了图灵奖。）

当时的人们并不知道谁会是最终的赢家。提出关系模型的IBM，甚至还在把层次数据库IMS作为主力。

一直到IBM在1983年对外公开关系型数据库DB/2，才算是最终宣告了“关系派”的胜利。

要说“关系派”最终到底是凭什么战胜了“网状派”，可能只是因为占最大市场份额的数据库是“关系派”的吧。

*写时发现有点束手束脚，因为没有考虑到一个问题——科普文和技术讨论是完全不一样的。我试图尝试在一篇文章中融合这两种完全不同的受众，以至于两者都会觉得信噪比有点低。为了试图挽救，我在上篇相对照顾没有相关技术背景的读者，而下篇反之。*

参考文献：
- A Relational Model of Data for Large Shared Data Banks (E. F. Codd)
- What Goes Around Comes Around (Michael Stonebraker, Joseph M. Hellerstein)
