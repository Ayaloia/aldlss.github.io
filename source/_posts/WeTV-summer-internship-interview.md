---
title: 腾讯视频前端暑期实习面试经历
date: 2024-04-29 21:19:23
author: 又收到了 offer 的 aldlss
categories:
    - 回忆
tags:
    - 面试
    - 实习
updated: 2024-05-03 18:06:00
description: 运气又很好
---

因为可能面试内容能写的比较少，主要大概写一下面试经历。

<!-- more -->

# 前

为什么投这个呢？首先说为什么要投，主要一个原因是周一的时候收到了之前申请的绩点排名，发现这个排名非常不利啊。
众所周不知，我是还是想读研尤其是保研的，但是一看这个排名，其实就知道很难保，即使是保上了也是顶多保本校甚至不一定是本专业了。这个其实是非常难接受的，之前本来是想就关于我为什么想读研的一些相关问题写一篇文章的，但是还是懒得写了，现在看来其实也没什么写的必要。

总的来说就是反正暑假估计是没什么夏令营了，保研估计也是指不上了，但是考研也不想考，这样不如就看看就业吧。反正也不是说就业了就不可能继续读研了，我有位比较敬仰的学长就是上了一年班之后继续出来读研的，虽然说少，但还是有机会的。

那么投什么呢，字节算是体验了去过了，所以其实还想体验一下别的公司。除了字节以外我比较有好感的国内的公司就是腾讯了，因此选择了腾讯。
不过腾讯这个还有很多部门可以选择，听说 WXG 是最好的，但是我对微信还是不喜欢的，所以没有首先意向这个（当然人家也不一定要我）。
其实我是不认为我应该之后一直做前端的，所以还是想转一下别的方向，比如说就是想尝试一下音视频方面的，于是就意向部门就选择了腾讯视频，虽然岗位还是前端，但还是希望借此多少接触一下音视频相关的东西嘛（最后事实证明我错了）。

于是出排名的当天就补充了一下简历，主要是把字节的实习经历补充上去。然后就在腾讯校招上填信息投简历了。
投了之后要做一个什么综合测评，挺无语的，还要求摄像头之类的。做完下来感觉前面的都是那些 PUA 题目之类的，懂你意思；后面的都是很申必的感觉像是脑筋急转弯之类的智力题，这个还真大部分都想不出来，给的时间还少先，真的抽象。

# 一面

周一投的，结果周三晚上就来找我约面了，不得不说相对于我上次猛泡十天池子还是很快的，约了周四下午。
虽然东西都忘了很多，结果反而不是很慌的样子，晚上还猛打以撒。第二天也是比较不慌，不过大概也是看了一下一些之前面试字节标记的一些面试题之类的，以及还有复习了一下自己的简历，真的好久没看都忘了= =

也是找了间空教室准备面试，进去之后发现面试官已经到了，题目都出好了——顺带一提，面试用的是腾讯会议，好像有个类似插件的东西叫面呗可以用来写代码之类的。

1. 大数相加
嘛，先做题目，就是大数相加。我问必须 js 或者 ts 吗，他说可以不用。那我就说那这个我用 python 就直接秒了啊。
结果大概是他愣住了，最后也是说 python 能承载的大数也是有限的（确实虽然基本无限），有没有好一点的办法。
其实我是知道大概要问高精度的，那就写呗。不过既然他说可以不用 js，那我就上 c++ 了，感觉 c++ 处理字符和数字之间的关系还是比较舒服的。
反正就是写了个大概的，似乎又把他唬住了。最后也是提醒了一些其他的情况，比如说读入错误或者有很多前导 0 的情况。
估计有些是准备让我用 js 然后用正则或者什么的，结果给我用 c++ 字符嗯上了- -
虽然最后适配一些极端情况的时候出了点 bug，不过大概还是过了。

2. 自我介绍
是的，写完题目后才开始自我介绍。也是很久没有自我介绍了，真忘了大概应该该怎么说，说得也是挺磕磕巴巴的，不过也就是背简历嘛，还好还好。

3. 项目介绍
那就介绍吧，说得最多的就是我那个原曲认知测验的项目，毕竟这个项目我也是从 0 开始手写的，很熟悉也遇到过不少技术难题，能说的也是不少的。主要记住了两个能说的地方，一个是首屏夜间模式的切换，一个是音乐的生产消费模型。
不过似乎他们总认为我这个是听音识曲相关的软件，每次都要再解释一下才行（

4. 八股
唉剩下的就是八股了，懒得写，后面统一写一下吧。

5. 反问
反正就反问嘛，也是问了两个经典的问题，一个是面试评价，另一个是小组的业务。结果我原本以为会跟音视频编码的沾点关系，没想到是一点不沾啊。那边还详细跟我介绍了一下音视频编码那边的主要是技术研发岗，然后这边是业务岗，钱可能会多不过也要看产品做得好不好之类的。还建议我认真考虑一下到底想不想做业务之类的，感觉还是挺友善的？
哦对了他还建议我之后写代码尽量还是用 js 或 ts 写，难绷。

# 二面

一面完之后刚好寻思有带电脑嘛，就觉得刚好把认知测验的视频录了，然后周末发布一下。结果也是搞了挺久，搞到晚上才搞好。
结果一摸手机，发现打进来了好几个腾讯的电话，估计是约面的。本来下午看到过两个，但是当时没注意，等了也没来，于是就设置非静音了。结果晚上搞完发现刚错过又一个，我草原来是我勿扰模式没关，麻。
于是打之前约我面那位朋友的电话，答曰不是他打的，不过似乎他旁边有那个要约我的人，于是就约了一下时间。本来他是考虑明天晚上的，但我明晚感觉有点来不及。结果他说要不就现在，诶那我寻思还真行，毕竟电脑都已经带过来了，每次面试都要带电脑还是很麻烦的。
于是就约了现在。

1. 自我介绍
是的还是自我介绍，有了下午的经验感觉还是流畅了一点。不过他还是关注了两点，一是我的户口以及意愿工作地，二是我的读研意向，还好这两个前者我是和深圳挺配合的，后者我已经完全想过怎么答了。

2. 项目
好像问了项目吧，好像又没有？真记不得了= =

3. 八股
是的又是八股，甚至他还看了前一面问了哪些，有些再问了一遍，牛逼。

4. 情景题：2G 内存存储一亿个 10 位数 QQ 号，随机询问一个 QQ 号是否存在在里面
一开始只想到用 Trie 树，后面经过提醒说可以把内存当做数组才顿悟。
我草还有这种操作，简单来说就是把 QQ 号当做内存的位地址，读取内存那一位是不是 True 就行了。
真有点说法的感觉是。

5. 反问
感觉真有点快？可能九点了那边也急着下班。
反问就一个也是面试评价，另一个是关于他们部门或者说小组的一些问题，他们做的会涉及到金钱相关，于是我就想问问会不会有风险，结果答曰有专门的部门控制的，这样想大概是调库吧（
至于面试评价这个，他说我知识点比较零碎，跟我说通过实操学习固然好，但是覆盖面不够广，建议我看红宝书学习一下，我后来看了一下，应该是 js 的一本经典教程。

# 三面

二面也是很快通过了，结果三面就比较申必，电话也没打过来商量，就突然约了下周三晚上，有点久……要等快一周。
当天也是找了同样的教室，似乎六楼人都比较少啊。

1. 自我介绍
很熟练了。当然他也问了户口和读研的问题。

2. 选一个项目介绍
    那当然是我最熟悉的原曲认知测验。大部分都是问我有什么特点或者难点之类的，然后我说然后他就要么根据我说的问一下要么就继续问我还有什么，问到后面真的都燃尽了，感觉没什么了都。不过好在整个项目都是自己写的，顺着脉络讲下去总会有什么想起来的。
    这里就不细说了，懒得写，以后都靠临场发挥吧（

    哦有一点值得记录一下的，就是关于音频切分这块，他似乎有逻辑切分和物理切分两种方案，物理切分大概就是我现在这种，逻辑切分我有点没懂是怎么实现，虽然他跟我说了一个名词，但是我忘了（
    有机会查一下？（这样说大概就是没机会了）

3. 反问
照例问了几个问题，面试评价以及部门和小组的情况。

只能说看起来这位确实比较忙，半个多钟就结束了，我一度以为要凉了。

# HR 面

HR 面没什么说法，过了几天就约了上午快中午的时候。

主要就是问了地域、入职时间和读研之类的的问题，还问了一下我又没有在投的。其实我是没有的，但看说没有的可能不好，于是编了几个，但追问之后我有点说不出来了，感觉被她看破了（
然后就直接说准备发 offer 了，打完后过会又再打过来了原来是忘说薪资了。不过没想到腾讯是按月给的，我还以为都是按天结算。

关于反问，就主要问了一下同一小组部门中不同地域的区别。
不到十分钟就结束了。

# 后

其实后面才发现还有很多应该问的忘问了，比如三餐包不包，转正率怎么样之类的。唉当时也是没怎么调查，谁知道好像真不包午餐啊，转正率听说也很寄的样子……这样写着写着突然就有点不想去了（
不过已经接了，当时接的时候好像也是比较激动吧。
![WeTV-offer](https://cdn.suwako.cn/aldlss-blog/pic/WeTV-offer.png)_offer 邮件的部分截图_

不过转不转正倒也无所谓了罢，也是权当体验了，这样想来，果然还是得多调查一点？最近很多事情都没仔细调查了解过啊……感觉没有信息还是不行的。

接下来简单总结一下提到的一些八股：

1. 浏览器渲染流程
2. 输入网址后发生的事
3. JS 任务运行机制
4. TCP 建立与断开，与 UDP 的差别等
5. 计网七层模型/五层模型
6. ES6 的新东西（这个我都不太好说，因为我学的时候就是直接学 ES6 后的了）
7. 学过的数据结构
8. 进程线程
9. HTTP 各版本的一些特性
10. JS 原型链、继承
11. JS 闭包以及怎么实现
12. 图片编码格式，尤其是比较新的
13. XSS
14. KMP

后面上牛客看了一下发现还真有人跟我面到同一个组了，题目有些都是类似的，而且面试的日期还跟我差不多。不过他挂了，希望不要是我把他挤挂了。

# 结

怎么说呢，有时候从面试的难度或许可以看出组的整体技术水平？

填写入职信息的时候，看到要用微信扫码填写的时候我是无语的，真的是 All in WeChat 了啊，讨厌的感觉。
但感觉这个时候还是不要凭喜好了吧，虽然作为一个整体可能不喜欢，但跟里面的细分的地方和人其实大概是没关系的。
希望还是不要后悔就好。

最后，也是再次希望看到这里的各位也能获得自己心仪的 offer 吧。