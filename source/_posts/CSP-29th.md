---
title: 第 29 次 CSP 认证部分题解及踩坑
date: 2023-03-21 20:19:40
author: 感觉还行的 aldlss
categories:
- 心得
tags: 
- 比赛
updated: 2023-03-22 10:46:46
description: 狠狠踩坑
---

这次不是游记了，也是这次题比较给面子，写了个 300 分以上，所以想着写一下。不过其实主要是想写一下后面踩的一个坑。

<!-- more -->

## 土地丈量

这题呢，只能说得亏前几天写别的题目的时候写过类似的题，不然还真不会。

本题是要求出一块大田地和其他 n 块田地的重叠面积，因为题目说 n 块田地之间不相交，其实剩下了很多麻烦，就不用考虑 n 块田之间有重叠导致面积重复计入的问题了。

因为数据量也比较小 (n <= 100)，所以可以直接分别求是否重合，重合的话直接求面积。

判断是否相交其实很简单，就是最大的横纵坐标比另一个的最小的小，或者最小的横纵坐标的比另一个最大的大。

至于判断重合面积，是用两个矩形的总共四个横坐标选中间大小的两个作差，与它们的四个纵坐标中间大小的两个的差相乘。虽然写起来比较简单，但是我仍然不知道这到底是怎么能想出来的- -

还是贴代码吧，我是用类的写法写的（不知道为什么总感觉挺合适）：

```cpp
#include"bits/stdc++.h"
using namespace std;
class rece 
{
    public:
    int minx, miny, maxx, maxy;
    rece() = default;
    rece(int x1, int y1, int x2, int y2) {
        minx = min(x1, x2); // 分别求出最大最小的横纵坐标
        maxx = max(x1, x2);
        miny = min(y1, y2);
        maxy = max(y1, y2);
    }
    bool isJiao(rece &b)
    {
        if(minx >= b.maxx || miny >= b.maxy || maxx <= b.minx || maxy <= b.miny)
            return false;
        return true;
    }
    int jiaoArea(rece &b)
    {
        int x[4]={minx, maxx, b.maxx, b.minx}, y[4]={miny, maxy, b.maxy, b.miny};
        sort(x, x+4); // 其实这里按理说用归并大概会更快，不过就这点复杂度就懒了（
        sort(y, y+4);
        return (x[2]-x[1])*(y[2]-y[1]);
    }
}reces[105],me;
int n, ans;
int main()
{
    int x, y;
    scanf("%d%d%d", &n, &x, &y);
    me = rece(0, 0, x, y);
    int a, b, c, d;
    for(int i=1; i<=n; ++i)
    {
        scanf("%d%d%d%d", &a, &b, &c, &d);
        reces[i] = rece(a, b, c, d);
    }
    for(int i=1;i<=n;++i)
    {
        if(me.isJiao(reces[i]))
            ans += me.jiaoArea(reces[i]);
    }
    printf("%d", ans);
    return 0;
}
```

## 垦田计划

这个不多说了，基本上写每题的时候我都会比较首先想这题能不能用二分答案，没想到终于在这里碰上了能用二分答案的题目，感动。

一道题能不能二分答案，大概有两个要求：

1. 一般是最优解问题，而且可能的答案集是可二分的。不过说人话一点，大概就是，一个范围，一边都是不可行解，另一边都是可行解，它们的交界处是最优解。

2. 根据可能解判断是否符合题目比直接求解复杂度更低。这个某种程度上说也是二分答案的目的。

然后比较显然的是，这题是可以二分答案的，具体就是二分 k ~ t<sub>Total</sub> 这个范围，然后判断是否是解就可以了。其中有一个坑就是求缩短了多少天时，因为估计的答案比较大，相减时会出现缩短天数得负数的情况，这个肯定是要判断变成 0 的。

以下是代码：

```cpp
#include"bits/stdc++.h"
using namespace std;
struct tian
{
    int t, c;
}tians[100005];
int n, m, k, ans;
bool judge(int w) // 判断答案是否可行
{
    int sum=0;
    for(int i=1; i<=n; ++i)
    {
        sum += (max(0, tians[i].t - w)) * tians[i].c; // 这里就是可能出现负数的地方
        if(sum >= m)
            return false;
    }
    return true;
}
void ef(int l, int r) // 二分答案
{
    if(l > r)
        return;
    int mid = (l+r)>>1;
    if(judge(mid))
    {
        ans = mid;
        return ef(l, mid-1); // 我是比较喜欢用这种写法
    }
    return ef(mid+1, r);
}
int main()
{
    scanf("%d%d%d", &n, &m, &k);
    int maxx=0;
    for(int i=1;i<=n;++i)
    {
        scanf("%d%d", &tians[i].t, &tians[i].c);
        maxx = max(tians[i].t, maxx);
    }
    ef(k, maxx);
    printf("%d", ans);
    return 0;
}
```

## LDAP

第三题终于不是终极数据结构套数据结构套数据结构了，令人感动。这个我认为是字符串处理的题目，虽然挺不喜欢的，但是好像意外地比较好写？

我直接说说我的看法，首先，它这个还是挺人性化的，给了范式，可以看到表达式说起来的话只有两种可能。一种是 `BASE_EXPR`，我认为可以说是原语；另一种就是 `EXPR`，也就是复合语句，复合语句的一个特点就是它是以 `&` 或者 `|` 为头，后面跟两个括在括号里的式子，而括号里又是同样的复合语句或者原语。

很容易想到我们可以用递归来解析整个表达式。具体流程是这样：

1. 首先我们检查获得的表达式的第一个字符。这种情况下，只有两种可能，一种是字符为 `&` 或者 `|`，这说明这个表达式是个符合语句，否则它就只可能是原语。

2. 若是复合语句，则我们分别找出最外面的两组括号，它们分别参与第一个字符的操作符运算的表达式。由于显然第二个字符是 '('，最后一个字符是 ')'，所以我们只要找出中间的分界即可。我这里是使用的直接暴力查找的方法。

3. 找出来之后，对两个表达式内部分别调用递归函数，即回到步骤 1 继续处理内部，将返回的值按照第一个字符进行与操作或者或操作

4. 若是原语，则直接按照原语的构成，先读一个数字，再读符号，再读一个数字，最后根据符号和数字判断和 user 的属性是否匹配，返回 `true` 或 `false`

在递归表达式上，因为技术原因，我是用 l, r 值来控制表达式的起止位置（闭区间）。

对于怎么判断每个用户是否符合条件，我是直接一个一个枚举过去的。这样其实对一个表达式重复解析了多次，有很大的优化空间，因此也很忐忑能不能过，但倒是过了。然后由于答案要求按用户 DN 大小从小到大输出，于是我们可以在只在最开始排序一次，然后枚举的时候加入答案的顺序也是有序的了。

另外听说有一个坑是属性编号和大小的范围与 n, m 的范围不同，是 10<sup>9</sup>，不过还好我用的是 `unordered_map`，没有被这个坑到。另外就是我觉得在数组中套一个会变大变小的数据结构可能是比较危险的，因此可以看到我在声明 users 数组的时候用的是指针，这样数组里存的就只是一个 `int64` 的指针liao

```cpp
#include"bits/stdc++.h"
using namespace std;
struct user
{
    int DN;
    unordered_map<int, int> attribute;
};
array<user*, 2505>users;
int n;
vector<int>ans{};
string expr;
bool parse(int l, int r, user* me)
{
    if(expr[l] == '&' || expr[l] == '|') // 判断是否是复合语句
    {
        int count=1;
        for(int i=l+2; i<=r; ++i) // 查找两个子语句的分界
        {
            if(expr[i] == '(')
                ++count;
            else if(expr[i] == ')')
            {
                --count;
                if(count == 0)
                {
                    if(expr[l] == '&')
                        return parse(l+2, i-1, me) && parse(i+2, r-1, me);
                    else
                        return parse(l+2, i-1, me) || parse(i+2, r-1, me);
                }
            }
        }
    }
    // parse Base_Expr
    int a[2]={0, 0}, point=0;
    bool logic; // false='~', true=':'
    for(int i=l; i<=r; ++i) // 这里用了比较方便的写法，但是不太易于理解，只能说 ^=1 确实是个好东西
    {
        if(expr[i] == ':')
        {
            logic = true;
            point ^= 1;
            continue;
        }
        if(expr[i] == '~')
        {
            logic =false;
            point ^= 1;
            continue;
        }
        a[point] *= 10;
        a[point] += expr[i] - '0';
    }
    auto res = me->attribute.find(a[0]);
    if(res == me->attribute.end())
        return false;
    if(logic)
        return res->second == a[1];
    return res->second != a[1];
}
bool cmp(user *a, user *b)
{
    return a->DN < b->DN;
}
int main()
{
    scanf("%d", &n);
    int m, a, b;
    for(int i=1; i<=n; ++i)
    {
        users[i] = new user;
        scanf("%d%d", &users[i]->DN, &m);
        for(int j=1; j<=m; ++j)
        {
            scanf("%d%d", &a, &b);
            users[i]->attribute.emplace(a, b);
        }
    }
    sort(users.begin()+1, users.begin()+n+1, cmp); // 先排序，这样子后面的答案就直接都是有序的了
    scanf("%d", &m);
    ++m; // 配合后面 --m
    while(--m) // 这样写比 m-- 亲测快很多倍，不过如果吸氧的话就不懂了
    {
        cin>>expr;
        ans.clear();
        for(int i=1;i<=n;++i)
        {
            if(parse(0, expr.length()-1, users[i]))
                ans.emplace_back(users[i]->DN);
        }
        for(int &w:ans)
            printf("%d ", w);
        puts("");
    }
    return 0;
}
```

## 施肥

第 4 题没写，没思路，咕了。第 5 题其实也没思路，但是我这些这篇文章的目的其实就是这题- -

也不解析题目了，首先我是写了一个巨麻烦的实现，写的时候各种高级数据结构飞来飞去，结果最后只有 15 分，后面三个 point WA 其他 TLE 了，笑嘻了

于是决定直接上暴力，当然也是有点脑子的暴力。具体说法就是答案的起始点只可能是某个施肥车的起始点，终止点同理。因此枚举施肥车的起始点和终止点，然后再枚举每个施肥车，看其范围是否被包含在里面，是的话使用差分的思想，在施肥车起始点 +1，终止点后一位 -1。枚举完之后再枚举起止点上的每一块地，并同时求前缀和，只要和为 0，就说明没有车覆盖到这里。否则如果直到最后都没有为 0 的和，就说明这段地可以被完整覆盖。另外值得注意的是，由于起止点可能有重复的，因此需要能判断重复并去重。

我一开始的去重思路是我之前听一个大佬讲把怎么两个用户的聊天当作的一个群聊的时候听说的，大佬说的大概是通过位运算把两个用户的 id 拼起来作为群聊 id，这样既不会和已有 id 重合，又可以作为群聊 id。考虑到 l, r 都是 32 位的，因此我考虑到直接将 l 左移 32 位再与 r 相或，这样构造的值是不可能与其他不一样的值构造出来的相冲突的，然后把这个值送进 `unordered_set` 里，就可以方便判断是否重合了。

最开始的代码如下：

```cpp
#include"bits/stdc++.h"
using namespace std;
int n, m, ans;
int st[200005],ed[200005];
int tian[200005];
unordered_set<long long>exist;
inline bool isExist(long long st, long long ed)
{
    return exist.find(st<<32 ^ ed) != exist.end();
}
inline bool pushExist(long long st, long long ed)
{
    exist.emplace(st<<32 ^ ed);
}
bool judge(int &stt, int &edd)
{
    memset(tian, 0, sizeof(tian));
    for(int i=1; i<=m; ++i) // 枚举每个施肥机
    {
        if(st[i] < stt || ed[i] > edd)
            continue;
        ++tian[st[i]];
        --tian[ed[i]+1];
    }
    for(int i=stt; i<=edd; ++i) // 枚举起止点中的每个地块
    {
        if(i != 0)
            tian[i] += tian[i-1];
        if(tian[i] == 0)
            return false;
    }
    return true;
}
int main()
{
    scanf("%d%d", &n, &m);
    for(int i=1; i<=m; ++i)
    {
        scanf("%d%d", &st[i], &ed[i]);
    }
    for(int i=1; i<=m; ++i) // 枚举起始点
    {
        for(int j=1; j<=m; ++j) // 枚举终止点
        {
            if(st[i] >= ed[j])
                continue;
            if(isExist(st[i], ed[j])) // 已经存在的就不用判断了
                continue;
            if(i == j || judge(st[i], ed[j]))
            {
                ++ans;
                pushExist(st[i], ed[j]);
            }
        }
    }
    printf("%d", ans);
    return 0;
}
```

PS: 刚刚才发现，应该把 `pushExitst` 函数放到 `if` 外面好点，因为无论结果是否是答案都是判断过的了，都不用再次判断了。

在本地跑了一下，令人惊讶地还挺快，比我之前写得感觉不暴力的那个快很多，能多得二十分的样子。

结果满怀期待地交上去……

TLE 了。

当时也不理解，最开始以为是 `int` 强转 `long long` 性能有问题，改成了如下方案：

```cpp
inline bool isExist(int &st, int &ed)
{
    return exist.find(st<<16 ^ ed) != exist.end();
}
inline bool pushExist(int &st, int &ed)
{
    exist.emplace(st<<16 ^ ed);
}
```

虽然可能有冲突的风险，但是在当前数据量下大约冲突概率为 0，试了试样例，也没有问题，于是交了上去。

结果还是 TLE。

想到反正还有那么多提交次数，也快没时间了，于是只能一个个注释掉一个个试，当把 `unordered_set` 相关代码注释掉后，就变 WA 了，我以为是 `unordered_set` 性能问题，虽然我在之前那个代码也是这样写的却没有这个问题，但目前的检测看来就是这样，于是只好把 `unordered_set` 换掉，换成了感觉更节省空间也更快的 `bitset`.

改动后代码如下：

```cpp
bitset<10000007> bs{};
// unordered_set<long long>exist;
inline bool isExist(int &st, int &ed)
{
    return (bs[(st<<16 | ed)%10000007] == 1);
    // return exist.find(st<<16 ^ ed) != exist.end();
}
inline bool pushExist(int &st, int &ed)
{
    bs[(st<<16 | ed)%10000007] = 1;
    // exist.emplace(st<<16 ^ ed);
}
```

同样过了样例，然后同样交了上去，然后同样…………

哦，这次不是 TLE 了，是 RE

？

我只能说真给我 confused 到了，最后也是各种微调都无济于事，只好 15 分黯然离场。

晚上的时候请教了大佬和老师，答曰可能数组开太大了，导致复杂度比较大，我是比较疑惑的，这数组还好吧？至于说 `memset` 复杂度大，我觉得这种函数应该都会被优化得比较好的说。

然后也看到了 ACM 大师的指点，说如果 RE 的话，可以本地开 O2 试试。我这才想起来评测的环境是有开 O2 的，我一试，我草还真是，为啥啊？这真的是万万没想到啊，我的好兄弟 O2 居然背叛了我，程序居然吸氧吸似了。吸氧之后调试虽然爆了但是也没显示爆在哪，只好继续看看有什么其他方法。

问了问 newbing，说可以开 `-Wall` 编译选项。

我按下了构建，也几乎是同时，我在问题列表里看到了这一行

![waring0](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/picQQ%E5%9B%BE%E7%89%8720230321220723.png)_噔噔咚_

同时，构建系统也爆出了警告

![waring1](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/picQQ%E6%88%AA%E5%9B%BE20230321221234.png)_噔噔噔噔咚_

我草？

仔细一看警告所指示的代码……

```cpp
inline bool pushExist(int &st, int &ed)
{
    bs[(st<<16 | ed)%10000007] = 1;
    // exist.emplace(st<<16 ^ ed);
}
```

我草，为什么我这个函数是 `bool` 啊！？

我想起来了，我是复制黏贴的上面那个函数啊！

把 `bool` 改成 `void` 后，运行就不报错了，令人感叹。

20 分……20 分要逃走了！不对，是已经逃走了呜呜呜……

所以总结下来大概是我写了一个返回值为 `bool` 的函数但是没有写返回值，这个在正常编译下恰好还能跑起来，但是在 O2 优化后就爆掉了，估计是按照有返回值这样优化了之类的。

这件事告诉了我三件事：

1. O2 不是我最好的朋友。

2. 本地测试时要考虑评测时的编译选项和环境。

3. 要注意看警告。之前一直也比较忽视警告，这下是终于栽在这儿了。经过大佬点拨，我收获了 `-Wall` `-Wextra` `-Wshadow` 等编译时报警告的选项，以及 clang 的有个 `-Weverything` 的选项。要说的话 `-Wshadow` 的 shadow 指的是内层作用域变量覆盖了外层作用域变量，有时候在警告里确实会见到 shadow 这个词，这个选项是警告这个的，据说在巨大多复制代码的情况下比较有用。其余的就不太清楚了。

只能说教训还是比较深刻的。

![555](https://fastly.jsdelivr.net/gh/Ayaloia/ImgHosting/picQQ%E5%9B%BE%E7%89%8720230321223041.gif)_😭😭😭_