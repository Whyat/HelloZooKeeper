# 开篇：免费开源的趣讲 ZooKeeper 教程（连载）

<img src="https://cdn.jsdelivr.net/gh/HelloGitHub-Team/HelloZooKeeper@main/cover.png"/>

<p align="center">本文作者：HelloGitHub-<strong>老荀</strong></p>

## 一、起因

> 良好的开端，是成功的一半。

我是作者[老荀](https://github.com/kaixinbaba)，一个普通的程序员，没有 985 和 211 的背景，也从没在大厂工作过。仅仅是喜欢研究技术，一直想做一个讲解技术的完整系列。然后我加入了 HelloGitHub 开源组织，在大家的鼓励和帮助下，我开启了讲解系列。

经过和蛋蛋讨论，最终确定了这次系列的主题是顶级开源项目 ZooKeeper 以下简称 ZK。

> ZooKeeper 是 Apache 软件基金会的一个软件项目，它为大型分布式计算提供开源的分布式配置服务、同步服务和命名注册。 ZooKeeper 曾经是 Hadoop 的一个子项目，现在是一个顶级独立的开源项目。

选它的原因如下：

- ZK 我曾经大概是在去年的时候，有深入研究过一段时间，只是当时没有做过多的记录，就自己随便看看，但是没能整理出来，心里总留着一丝的遗憾

- 我本身是 Java 程序员，所以从阅读理解上来说，还是看 Java 的代码最亲切，最舒服，而且我已经练就了一定程度的肉眼 DEBUG 能力，不需要将程序运行起来就能在脑中推导整个流程

- ZK 本身是一个基础的协调框架，而且其他编程语言也有对应的客户端，所以受众比较广，并且 ZK 本身架构是分布式的，具有一定的复杂性，非常值得学习

- ZK 市面上的书本资料很少（相较于 MySQL 或 Redis）而且基于的也是 ZK 的旧版本（不是最新版本），我想尽自己所能为开源社区添砖加瓦

![](./images/1.gif)

## 二、介绍

> 系列文章基于当前 ZK 最新的版本：3.6.2

这个系列还是延续 HelloGitHub 的 Hello 宇宙，起名为 「HelloZooKeeper」。文章大致分几个部分来讲解：

- 基本介绍（安装和使用）
- 业务处理流程
- 数据内存模型
- 选举
- 会话管理
- 持久化 & 协议
- 面试题
- 配置大全及其他 ZK 的隐藏功能

差不多就以上这些主题，又因为 ZK 本身的话题还是比较大的，另一方面受限于本人水平，没办法做到事无巨细、面面俱到，所以之后如果有补充我会做成单篇文章，添加进去。

<img src="./images/2.jpeg" style="zoom:80%;" />

## 三、内容

> 不积跬步，无以至千里。
>
> 不积小流，无以成江海。

讲解原理难免会和枯燥挂钩起来，我和蛋蛋也在交流到底是怎么样的形式才更容易让大家接受，而我们的目标就是希望大家都能通过我们的文章有所收获，所以这一次：

- 采用基本不讲解源码的方式来讲解 ZK 的原理

- 在讲解的过程中我自己会虚（chui）构（niu）一个生动的小故事帮助大家理解

- 尽量用通俗、幽默的语言把一个个复杂难懂的知识点讲清楚、讲明白

- 以图为主，文字为辅的方式，尽量减少读者的阅读负担

- 在文章中时不时穿插一些我认为很搞笑的网络梗、表情包，进一步提高读者的阅读兴趣

<img src="./images/3.gif" style="zoom:80%;" />

开始之前，有两句话想要说在前面：

文章中的观点不一定是客观的事实，但是都是本人通过源码推敲得出的结果，至少在本人**主观的认知上都是正确的结论，尽最大的努力对读者负责**。所以，有问题欢迎大家指出和讨论，不要留一句：“垃圾”就走了。这是不负责任的表现！

开始动手写该系列的时候 ZK 最新版本是 3.6.2，如果在写的过程中 ZK 迎来重大升级，**怕不是在玩我？讲解的版本号不会做变动**，针对有必要的新特性，会在之后的单篇中进行单独介绍。为了兼顾有趣和深度，文章中举的有些例子未必是准确的，只能说是尽量贴近事实的同时会省略一些不重要的流程，从而减少读者的阅读负担。


## 四、展望

> HelloGitHub 因你们而精彩

既然是 HelloGitHub 出品的系列，怎么能少了和 GitHub 的梦幻联动呢？

我们会提供一个仓库用来存放文章，希望大家可以把关于文章的建议或者关于 ZK 相关的讨论，在 issue 区留言：

> https://github.com/HelloGitHub-Team/HelloZooKeeper/issues/new

我一定会尽力回复每一位读者，同时如果有不少人都有疑惑的知识点，也会收集后通过单篇文章的方式，整理 issue 后统一解答。

请不要吝啬你们的留言，你们的留言很可能会帮助到其他有相同困惑的人，让我们一起来把 HelloZooKeeper 建设得更好吧～

各个阶段的小伙伴，都可以加入到**教程的编写和校审**中。欢迎：

- 新手：参与到修改文中的错字、病句、拼写、排版等问题
- 使用者：参与到内容的讨论和问题解答、帮助其他人的事情
- 老司机：参与到文章的编写中，让你的名字出现在作者一栏
- 不懂编程的小白：点个 Star 支持我们在做的事吧！

> 项目地址：https://github.com/HelloGitHub-Team/HelloZooKeeper

<img src="./images/4.jpg" style="zoom:75%;" />

**预告**：下一篇是安装和上手，带你进入 ZooKeeper 的世界。下周见！

## 五、最后

我是 HelloGitHub 的卤蛋：

荀哥儿是我们 HelloGitHub Java 技术群的群主，他是个资深 Java 程序员，不仅技术好、热爱开源还很幽默和谦逊。他经常在群里耐心地回答大家的问题，我说他一个人盘活了 Java 群，他却说：“别这么说，都是群里的兄弟们挺我！”

由荀哥儿编写的 HelloZooKeeper 系列，从筹划到最终发布用了 2 个月的时间，他为了让枯燥的文字变得风趣，自己画了 50 多张图+并插入了各种有趣的图片。为了保证连载不断，他完成了 9 篇才决定开始发布，期间还不断打磨提高文章的质量。对于我提出的修改建议，他都会认真考虑并在保持自己文章风格的情况下进行采纳。该教程还采用开源和开放的编写方式，方便大家贡献和运行，后面会有帮助理解的示例项目，相信大家一定会喜欢的。

讲解技术的连载文章往往都没有好看的阅读数，但 HG 会把这个系列（10+篇）从头到尾连载完成！不忘初心，由衷的希望读者能从《讲解开源项目》中学到东西，找到乐趣爱上开源。

HelloGitHub 感恩有你！

