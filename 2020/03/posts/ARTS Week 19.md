标题： ARTS Week 19
分类： ARTS
tags： ARTS
-----------------------------------

Mar 2, 2020 ~ Mar 8, 2020

### Algorithm
Problem 401. Binary Watch（二进制手表）    [题目链接](https://leetcode-cn.com/problems/binary-watch/)

题目描述：给定下面一个手表，灯亮表示选中，上面 4 个灯表示小时（0-11），下面 6 个灯表示分钟（0-59）。图中的时间表示 "3:25"。

![手表图](https://upload.wikimedia.org/wikipedia/commons/8/8b/Binary_clock_samui_moon.jpg)

给定一个数字 n，表示当前处于亮灯状态的数量有 n 个灯，返回可能代表的时间。注意：小时前面不需要含 0，分钟前面需要包含 0。
例如：n = 1
返回结果：["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]

思路为：亮几个灯可以视为是一个组合问题，比如在小时中，亮了两个灯，则表示从 4 个灯中选择 2 个进行组合，而后求和计算是否在范围内（0-11），内部 `combination` 函数便是用来计算给定列表的组合，而 `cal_hour_value` 和 `cal_minute_value` 便是分别计算小时和分钟的值，该函数中会进行范围检查并转化为符合条件的字符串，`combine_hour_and_minute` 函数用来将可供选择的小时和分钟拼接起来。

但是，我上面的所有的内容都是将小时和分钟的亮灯数目分开考虑的，而在题目中给定的 n 是一共的亮灯数，因此需要对 n 进行分解，如 n = 1 = 1+0 = 0+1，n = 2 = 2+0 = 1+1 = 0+2。不过要注意小时和分钟的灯的数目限制，例如 n = 8 = 1 + 7 就不存在，因为表示分钟的灯只有 6 个。

通过的代码如下：
```python
class Solution:
    def readBinaryWatch(self, num: int) -> List[str]:      

        def combine_hour_and_minute(hour: List[str], minute: List[str]) -> List[str]:
            res = []
            for i in range(len(hour)):
                for j in range(len(minute)):
                    res.append(hour[i] + ':' + minute[j])
            return res
            
        def cal_hour_value(n):
            arr = [1, 2, 4, 8]
            tmp = combination(arr, n)
            res = []
            for nums in tmp:
                t = sum(nums)
                if t < 12:
                    res.append(str(t))
                else:
                    pass
            return res

        def cal_minute_value(n):
            arr = [1, 2, 4, 8, 16, 32]
            tmp = combination(arr, n)
            res = []
            for nums in tmp:
                t = sum(nums)
                if t == 0:
                    res.append('00')
                elif 1 <= t <= 9:
                    res.append('0'+str(t))
                elif 10 <= t < 60:
                    res.append(str(t))
                else:
                    pass
            return res

        def combination(L, k): # C(n,k) = C(n-1,k) + C(n-1,k-1)
            if k >= len(L):
                return [L]
            if k == 0:
                return [[]]
            T1 = combination(L[0:len(L)-1], k-1)
            T2 = combination(L[0:len(L)-1], k)
            T = []
            for e in T1:
                e.append(L[len(L)-1])
                T.append(e)
            return T2 + T

        if num == 0:
                return ['0:00']
        elif num > 10:
                return []
        else:
            if num <= 4:
                res = []
                for i in range(num+1):
                    hour = cal_hour_value(i)
                    minute = cal_minute_value(num-i)
                    res.extend(combine_hour_and_minute(hour, minute))
                return res
            else:
                res = []
                for i in range(5):
                    hour = cal_hour_value(i)
                    minute = cal_minute_value(num-i)
                    res.extend(combine_hour_and_minute(hour, minute))
                return res
```

### Review
本周继续 Review 每个程序员需要知道的 97 件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：

- 二进制（One Binary） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_61/)
我们需要控制生成二进制文件的方式，如果每个开发人员都自行生成其相应的二进制文件，那么无疑是灾难的。同时，还需要保持环境信息的一致性，以避免一个人更新代码后而其他人仍在使用旧的代码，幸运的是，我们现在可以使用 `git` 等工具很容易的做到它

- 只有代码会告诉我们真相（Only the Code Tells the Truth） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_62/)
虽然程序最终以二进制形式运行，但二进制形式难以理解。因此源代码便是了解程序如何运行工作的最好方式。你需要精心的组织代码的设计，排版等，像文章/论文/诗歌等，这不仅有利于他人能够易于理解和掌握，而且有利于你自己过一段时间回顾时不至于难以理解

- 拥有（和重构）构建脚本（Own (and Refactor) the Build） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_63/)
一般的，项目的构建语言一般与项目使用的语言并不同，比如 C/C++ 项目中可能会使用 Makefile 来进行管理项目并构建，其他语言可能是 Bash 脚本等。除了要时常维护项目中的代码外，仍需要维护构建时的代码，尤其在您改变了项目中文件布局后。

- 结对编程并感到流畅（Pair Program and Feel the Flow） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_64/)
结对编程有很多好处：减少“卡车因素”，避免对某个成员的依赖；有效地讨论问题：当你遇到问题后，总会有人能与你讨论；平稳集成：结对编程时两个人可以相互为对方提供有效的 Code Review；缓解干扰：当其中一人必须离开时，另一个人可以继续工作；使新加入的人快速上手：通过给新人配备老员工，有助于新人快速熟悉项目。

- 首选领域特定类型而不是原始类型（Prefer Domain-Specific Types to Primitive Types） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_65/)
浮点数经常带来一些意想不到的问题，尤其在一些要求高精度的领域，比如科学计算/实验，金融等，我们更应该选用特殊类型来进行使用，而不是语言的自定义类型，语言的自定义类型更适合通用领域而不是特定领域

### Tip

Linux 中 `inode` 结构中存储了文件的元数据（例如：inode编号，所有者，上次访问/修改时间等）和数据部分（文件的具体内容），但是 `inode` 中 **并不存储【文件的文件名】**，文件的文件名存储在目录项缓存 `dentry` 结构体中。

### Share

本周终于从假期中走了出来，迈上了正轨，所做的工作量大致比前两周的和还略多一些，希望能下一周继续保持，争取在下一周初步完成，进入下一阶段。
