---
title: 飞书前端日常实习面经
date: 2023-12-19 17:36:00
author: 收到了 offer 的 aldlss
categories:
    - 回忆
tags:
    - 面试
    - 实习
updated: 2024-03-28 19:58:00
description: 运气很好
---

既然有了不错的结果，那么就寻思把整个流程记录一下吧。

<!-- more -->

# 前

为什么想投递，主要还是看到别人似乎大二大三猛实习了，而自己还一事无成，还是比较焦虑的。而且感觉寒假也没什么事的样子，而下学期开学后必定是没有时间的，寒假不实习就很难再有机会了。而且想着如果有段寒假日常实习无论对之后暑假实习还是可能申请夏令营应该都能有帮助吧，而且也能学到一些工业界的架构和正规流程之类的。

其实之前一直想投递的，但是因为我准备写到简历里的项目还在开发中，所以一直没有写简历。等到项目基本上完工的时候，已经到比较晚的时候了，好在很久之前其实就写过简历，当时就是卡在了写项目这一环节。后面用 React 手动重写了了一遍简历，调整了样式，结果还是在写项目经历的时候摸了好久——真的不知道该怎么写。而且当时也是因为一是当时觉得挺晚了，是不是来不及了；二是感觉自己也没什么准备，有点没信心，不知道能不能过。

最后是终于在 12 月初写好了简历，但要说投什么公司，我也是比较矛盾的。一是武汉的实习机会还是比较少的，我也不可能在别的地方实习；二是我有好感的公司也不多，这里并不是说喜爱或者什么申必的感情，而是愿意去工作的意向，这种东西说起来还是挺虚无缥缈的。我对字节有点好感也是因为我有一位很崇敬的学长之前就在字节工作过，而且感觉字节也比较“年轻”吧？然后投这个岗位的实习也是因为之前还有一位我也觉得挺厉害的学长也投过这个岗位，怎么说呢，大概都是跟随前人的步伐吧（笑）

投了，投了之后一开始还是比较紧张的，但没多久之后就觉得应该是泡池子了，也就没再管，继续写我的项目和作业去了。直到十多天后的晚上突然收到邮件说是 HR 想联系我没联系上，遂给我发邮件，才急急忙忙去看手机（当时手机放在别的地方充电），发现有两个未接电话，谔谔。
联系上之后就是沟通到岗时间等基础信息，话说 JD 上明明说是每周至少到岗四天，交流的时候说是至少五天有点震惊到了我，不过好在我还能招架下来。然后就是约面，约在了两天后。

约在两天后其实是考虑赶紧恶补一下一些八股，老实说 JS 基础知识我甚至没系统看过= =，全凭别的语言的编码习惯和 Copilot 的提示边试边写。然后还是看了一下之前那位学长的面经，当时真的感觉是遥不可及啊……

# 一面

唉第一次面试，还是比较紧张的，很多东西都没来得及准备和组织好。找地方，原本找了一间我挺常去的教室，结果刚好下午有人上课，只得遗憾离场。最后还是找了另一间以前没去过的教室，还担心会不会面试中途结果有人来或者要上课开班会什么的，还好是没有。

配环境，因为原生 css 其实写得少，于是就寻思配个 unocss 的环境，到时候写也好写一点。没想到的是飞书自己有一个代码编写模块，最后根本没用到配的环境。

1. 自我介绍
笑死，自我介绍根本没组织过，最后就是想到哪里说哪里了，基本信息、参加的比赛、在校成绩、项目，大概按照这个顺序说下去了，有点磕磕绊绊的（

2. 为什么选择前端，今后还会一直走前端吗，是怎么学习前端的？
一开始大概是些这样的问题，大概也是因为我简历有写一些后端项目的原因，或者是日常提问（
我的回答大概就是觉得前端写起来很快乐，准备一直走前端，边写边学习这样子，不是重点，略过。

3. 事件循环题
接下来就是写题目了，这个一下弹起一个代码框的时候还震惊到我了，我还以为写题要屏幕分享呢。
第一题是一个考察事件循环的题目，就是一堆 Promise、setTimeout 之类的，里面有 console，给出输出。只能说还好我之前专门恶补过这部分，还挺顺利地做出来了。原本以为还要写输出，结果面试官跟我说直接用注释写出结果就可以了。
嘛，写出来之后就问我大概是怎么考虑的，反正就是把事件循环那套跟他说了，就先执行一个宏任务，在把微任务执行完。

4. 任务队列和微任务队列到底有几个，分别怎么创建任务和微任务
可能因为我讲的时候就用的 “任务” 和 “微任务” 两个词，有点不明白还是怎么样，我就说我看文档是没有 “宏任务” 这个说法的，就是 Task，任务，还有 Microtask，微任务，就任务一个队列，微任务一个队列。任务取一个，然后把微任务的做完这样子。后面又问了哪些可以创建任务，哪些可以创建微任务，我就说任务主要就是代码块、还有 setTimeout、setInterval 这类的；微任务就是有一个 queueMicrotask 这样的函数专门可以创建一个微任务，还有就是 Promise，然后也不记得了。

5. 平常有用 Promise 吗，Promise 有哪些函数？
函数的话我就大概举了 Promise.all, Promise.race, Promise.resolve, Promise.reject 这几个。用法的话我就给了一个是我自己使用中就感觉 Promise 传递错误和正常值非常方便，直接 await 然后 try catch 就可以了。然后他就问我平常你就用 Promise 干这个？我就说了还有就是浏览器的一些 API，可以 await 返回 Promise，就可以异步执行，不至于堵住渲染（其实一开始不说这个是寻思这不就是基本用法吗，甚至不算用法）。

6. 为什么 js 是单线程
这个也是就顺着聊到了，我就用了我之前看到的一个例子，如果 js 是多线程，那么如果同时操控一个元素，那么就不好说以哪个为准。我还提到了 js 执行和浏览器渲染是互斥的，但讲的时候突然就有点说不清为什么是互斥的了，就大概搪塞了同时搞也会有问题，还好他没有细究。

7. 怎么理解 async, await
我就先说了 await，结合我的学习体验和理解聊了一下。就说其实是语法糖，尤其要注意的是 await 后面的和前面的其实是两个代码块，后面的就是在 Promise.then 里面的语句，还指出我之前就没理解是两个代码块，搞错了东西，然后说用 then 这样方便理解云云。至于 async 的话我说其实也是语法糖，就类似给函数的返回值包了一个 Promise<> 这样子。面试官后面还问我说所以是觉得用 then 好理解一些是吗，这问得我一愣一愣的，还以为有什么陷阱，就说理解大概是这样好理解点，但是写确实是 await 写得舒服点。结果还是不知道为什么要问我是不是用 then 好理解一点。

8. 括号匹配问题
就是一个 `((a + 1) + (b + 2)) + 3`，要求输出 `a + 1\nb + 2\n(a + 1) + (b + 2)`，一开始还给我看懵了，我寻思这什么描述都没有，我怎么知道要干嘛，然后问了，就是说是括号匹配，输出括号的东西。这就懂了。
开写，面试官从上一题就提醒我说可以切换 js 或者 ts 写，我假装以为是建议，继续用 c++ 写，结果就跟我说别用 c++ 写，用 js 或者 ts 写，也是要考察一下相应的代码水平的。好吧，没怎么用 ts 写过算法（js 就更算了，没写过一点），还好有代码提示。反正就是用栈，记录左括号的位置，匹配到右括号就出栈输出。不过题目还有一个例子是左括号多了的，那我就寻思先记录结果，然后最后看看左括号栈是不是空的，空的就成功，否则失败。
后面跟他讲解的时候还发现会有一个右括号多的问题，于是就是在前面匹配右括号的时候如果左括号栈为空，说明右括号多了，设置错误，然后 break 就得了。

9. 节流问题
大概是节流吧？反正就是有多次要发送的数据，希望能让它能一次发送完，而不是一个个发送。那我寻思就是计时，有发送的数据的时候先不急，等时间到了再发送，这段时间有其他的发送数据都加入到一个数组里，最后再一并。后面还被他点拨一下发完后要做什么，才发现数组发完后忘记清空了。

10. 拿苹果问题
有 100 个苹果，一次只能拿 1-5 个，怎么样才能赢？问了说是自己决定先手后手，那我寻思大概是有必胜法的。
我的思路是从低的往高推，不过还没总结出规律，他就问我了，我就直接跟他说了。1-5 个首先是肯定先手赢的，然后 6 个的话就是后手赢，7个的话就先手赢，拿 1 个就可以构造到 6 个的情况，8-11 也是如此，然后 12 就是后手赢……这样讲着讲着好像我也发现规律了，于是就下论断：苹果个数为 6 的时候，是后手赢，否则就是先手赢。

11. 反问
然后大概就是没时间了，我也看了眼大概 1 小时多了，于是就让我反问。我就问了两个：一是这是我第一次面试，您觉得怎么样，有什么可以指点的吗；二是您们具体业务是要做什么呢？
第一个问题他大概就回答说就感觉是挺聪明的，然后让我自信一点；第二个问题讲得有点多，大概记住的就是是写多维表格和一些逻辑的。听下来感觉还是挺有挑战性的，不是切图。

总体感觉面试官还是比较友善的，不过可能时间有点没把握准，一开始的时候说问项目的结果最后也没来得及问，好在题目不算很难。晚上的时候问了一下 HR，说是过了，于是约了后天下午面试。

# 二面

二面是真的出师不利，找教室的时候电脑合盖了，结果好不容易找到个空教室，电脑开盖后没反应了。当时就想是戴尔经典静电问题了，一开始还不慌，使用狂敲鼠标键盘大法，没反应，然后猛按电源键，还是没反应，当时就慌了。当时还有三十多分钟面试，终于等到还剩三十分钟的时候还没整好，于是我只得紧急收拾东西骑共享电车去实验室，到那边还剩十七八分钟。拆后盖拔电源放电一气呵成，还好确实是静电问题，不是给电脑电坏了。装好后盖和在后盖上拧不下来的螺丝，发现已经还剩八分钟了，就来不及拧剩下四个螺丝了，直接带电脑和电源就走了，走一半发现手机都没拿，也来不及去拿了，去三楼走廊找了个桌子椅子，打开会议，等待。顺便把时间同步了，然后插了电源。后来发现忘进入会议了，还好进去后面试官还没到，假装无事发生。

1. 自我介绍
这次有条理了点，按基本信息->学习成绩->竞赛成绩->项目这样子大概过了一下。

2. 预获取
没想到啊，一进来就单刀直入开始拷打项目，我一看时间才开始 6 分钟，应该是上一面没问项目的原因。第一个项目相关信息主要就是预获取了资源，反正是问我这个预获取是怎么个流程。我就跟他说是用消息队列，一边拿另一边收，消费者生产者模型之类的，反正扯了挺久，也估计是我没给他讲清楚的原因。

3. SSR
然后问我这个 SSR 是怎么做的，快了多少。我就说一开始就是 SSR，也不知道快了多少这样子。还给他提到可能会有日间模式、夜间模式不能马上加载的问题，他就说对啊这个怎么解决，我就提了真要说的我觉得可以用 Cookie 解决，根据 Cookie 不同发送不同的页面这样子，还说其实我的页面还好，没什么问题。他对我说用 Cookie 的方案有些困惑，不过最后也没纠结了，就举了另一个例子，说假设有个页面有四个部分，一个部分是用户信息，其他三个部分是都一样的模块，怎么使用 SSR，我就说用户信息可以用 Suspend 包裹起来，流式传输，其他的照常服务器渲染。结果他说不是，Suspend 是 React 的东西，然后又问我说假设有一个 Canvas，用户想一开始就直接先获取到这个 Canvas 的内容，怎么做——PS，这块我现在才反应过来这是不是就是飞书那边可能遇到的问题——我就说这样的话那就截图，先发送图片过去，他说后端怎么做，我就想到一个可以用无头浏览器来截图做，不过我是寻思着用户 Canvas 都有了，搞个图片不简简单单吗。最后也是没想到其他办法了。
这块虽然现在总结的时候还清晰点，但是实际上交流的时候感觉真的说的是特别零碎。

4. Go 语言相关
然后看我下一个项目，是一个宣传页面，就跳过了，到再下一个项目，Go 写的一个项目，现在想起来，写这个真的是一个错误，被拷打完了。
首先是问我 Go 语言设计的目的是什么，是为了解决什么问题，我就想到 “大道至简” 这几个字，就说语法比较简单，然后比较适合编写网络这样子。他说不是，这不是关键。最后我也忘了怎么说了，反正扯到 Go 的协程了，他又问我协程是怎么实现的，我就说 Go 调控的，大概是像线程那样控制上下文之类的。他问我上下文有啥。我草我怎么知道啊，支支吾吾了一下说应该有一些当前变量的相关信息吧。后面又问我知不知道 Go 之间怎么通信的，我说好像是管道通信，然后就问我管道通信，共享内存之类的东西，我草我怎么知道 Go 语言怎么做的啊，这不是面试前端吗？问我为什么管道比共享内存好，我就大概讲了写比较安全啊，由 Go 内部实现啊，他说不是关键，我又说内部实现是消息队列啊，他说那肯定是消息队列，我说不出来了。
后面又问我内存回收怎么说，我就说了分代然后遍历。他说这些是基本，现在垃圾回收运行时都有，那我也说不出来了。又问我怎么理解分代，分代的依据是什么，我就说了大概是时间，时间久的是老生代，时间短的是新生代，老生代不会经常遍历，新生代会遍历多点。然后问我怎么理解遍历的时候这个根节点，这真给我干懵了，这不就是 Global 吗，还能有什么，也是给了我些提示，我也没懂，寻思难道是函数上下文？他说不是。最后问我线程里有什么，我又懵了，什么叫线程里有什么，当时真懵了，甚至答了有代码块。后面他说了啥忘了，但是我就懂了，说按您的意思是根节点还包括线程？他说是的，跟我说根节点有 Global 和线程上下文（好像是这个，忘了），然后还跟我说三色标记法和一些专有名词之类的，问我知道吗，我说不知道啊，他就说你肯定没了解过，这些是无论 Node 还是 Go 什么的都是通用的，一开始 Java 用的什么垃圾回收方法太慢了，改进了之类的，然后就给我介绍了一下，当时真懵了，没理解到他说什么了。
我的点评，最拷打的一集，Go 的原理我是一点不懂，我怎么知道逮住我这个猛问，这跟前端关系是啥啊，想跳了。
补充一下，可能另一个原因可能也是因为这位同学好像是后端转前端的，可能是属于后端的记忆苏醒了吧。虽然我也是先写的后端，但是没有答出来感觉就很惭愧了。

5. 递归解析问题
然后就是写题，第一题是一个类似解析函数的题，问我大概的解法，我首先就是说从外往里，依次找大括号定义；然后问我用什么储存，我说可以用树，然后写了大概的结构定义，他首先问我如果求值里面又求了自己怎么办，也就是说递归调用自己了怎么办，中间走了些弯路，扯了一会最后得出应该是要记录调用的路径这样子。
最后问我如果函数递归调用太多了会发生什么，我说会栈溢出，他问我怎么解决，我说就改递归为非递归，因为递归用的是栈，就改成用 new 索取堆的空间（当时以 C++ 做的例子），就不会栈溢出了。对面好像不是很满意的样子，现在想来难道是想让我从里面往外面推（？

6. 小于 n 的最大值问题
给一个 n，然后给一个 A = {1, 2, 8}（假设），给出用 A 构造的最小的 n。举个例子，比如 n = 15897，那么得到的答案应当是 12882。我直接说了思路，刚要说发现不太对劲，不过他又问了，于是就说目前想到是贪心，拿最大的小于等于的数拼，但是这样可能会出现要回溯的情况。他对这点表示肯定，问我怎么解决。想了好一会没想出来，他就说有没有一个办法是能在前面就判断出可不可行的，我就说按您的意思那就是说可以用最小的数先拼出来试一下，不过后面我又说了一下我感觉这样还是要构造判断，感觉还是有时间消耗，他说他想的就是这样构造，问我难道是有更快的，我说没有，也没想到了。
然而又突然想到了，就说可以预先构造好，然后要判断的时候直接拼接就可以了，不用每次构造一个数。他没理解（
然后就是巨大解释环节，就跟他说我的想法是怎么样，他就还是没理解，说这样还是没什么区别啊。最后还是 show the code 了，写了个我的方法，这才说通了，说是预缓存的话确实快一点，我就说因为寻思每次都构造的话最多会是 O(n) 啊，他说不是这样算的（，不过确实也是快了一点

7. 反问
简单反问了一下，就是说觉得我表现怎么样，在飞书那边工作是要学习什么。第一点他说挺好的，但是原理方面要深入一点，不能只看别人的文章，要多看源码。第二点他说有点广泛，一时不好说，说如果到时候我能入职再说。

这之后就结束了，一看时间，跟上次也差不多，1 小时 15 分钟左右，好像看到面试官面试的时候有时前后晃来晃去，有点生草。总的来说现在想来好像都是被拷打，除了最前面跟他解释生产者消费者模型和最后一题的时候比较好点，其他的时候感觉都很寄。怎么跟我看的学长的面经完全不一样啊！React 没问，JavaScript 没问，问我 Go！？唉不过也是因为我往简历里面写了 Go 的原因吧。

晚上问 HR 怎么样了，也没回我，上次可是一问就回了，不知道这次是周五下班了的原因还是挂了，只能说令人感叹。

就这样忐忑不安地度过了周末，周一上午一醒来就看到微信 HR 跟我说二面过了的，不过 HR 面还要再等安排。当时就感觉有点稳起来了，但是看到等安排又寻思不会是开始排序了吧。当时也是要复习考试，于是也就没多管，开始复习考试了——说是没多管，其实当天晚上就刷了好几个钟牛客，后面每天晚上也都刷一阵子，看疯了。

嘛，本来寻思考完试就问问什么情况的，结果考完试一出来，发现 HR 已经问我某个时间点有没有时间了。当然是有的，于是就约了。

# HR 面

虽然很多人说 HR 面基本稳了，但是问了群友之后感觉还是需要提前考虑一些问题的。于是就学习准备了一下，本来也准备好了，结果突然又说面试的那个 HR 有事推迟了一个钟，问题不大。

当时发了一个新链接给我，等到一个钟后发现到点了还没人，有点小慌，寻思不会是原来那个面试链接吧。去看了，没有，结果回来的时候发现人已经在那了，好嘛该不会给人一个我比人还慢的印象吧，自然也是解释了一下。
对面好像说是网不好，于是就没开摄像头，中途还掉线了一次，不过问题也不大。

具体就不说了，大概都是些网上能找见的问题，基本都有准备过，除了少数由我的回答延伸出来的问题有点问到我了之外，都还好。结束后，大概看了眼时间，20 分钟，还挺快。

当时种种迹象让我闪过了一个念头，不会是 KPI 面吧！？唉面试时候对面说可能下周才能有结果，不安 desu。

# 后

就这样度过了不安的周末，一开始虽然是有点可有可无的心态的，但是都到现在这个地步了，确实是很心心念念了，周日晚上睡觉一直在想会不会像上周一样一醒来就看到发了 offer 的消息，又幻想拿到了 offer 后的成功生活，睡着后做了一个拿了 offer 的梦，醒了，然后又睡，又做了一个拿了 offer 的梦，只能说想麻了。

醒了，没有发 offer 的消息，于是问 HR，答曰这两天给答复。感觉有些不妙，莫不是真在猛排序？
当天做别的事的时候也一直时不时看看邮箱，或者想 Thunderbird 会不会给把 offer 邮件推给我，结果是没有。

醒了，早八，去上课。上到一半，看到来了一个电话。虽然归属地不是武汉，但是看着号码让我感觉非常相似，马上接了起来。
好嘛，是通知待遇之类的，准备发 offer 了，可能因为当时是上课，所以也没太激动吧，不过看到 offer 之后还是很兴奋了，毕竟怎么说，也是第一次嘛。
![lark-offer](https://cdn.suwako.cn/aldlss-blog/pic/lark-offer.png)_offer 邮件的部分截图_

# 结

怎么说呢，第一次投简历、第一次面试、第一次 offer、第一次实习，看起来全都是要给字节了。整个流程下来，虽有不安，但感觉还是幸运的。因为只投了字节，如果没过的话，真的就是寒假回家沉淀了，可能当时也是有点冥冥之中感觉能行吧。其中当然甚至是有些迷信的地方，但这些不太好说，也是怕说出来就不灵了。
最后，也是希望看到这里的各位也能获得自己心仪的 offer 吧。

---

现在也实习了几天了，就权当补充一下吧，可能能过的其中一个原因也是这边比较缺人。然后我加入的团队技术力这块确实是拿下了，不是单纯的切图什么的，很有挑战性，感觉是会很吃力的一次实习，具体的可能到时候会另外再写一篇心得？