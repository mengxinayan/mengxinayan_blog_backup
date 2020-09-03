标题： ARTS Week 9
分类： ARTS
tags： ARTS
-----------------------------------

Dec 23, 2019 ~ Dec 29, 2019
### Algorithm
Problem 69 Sqrt(x) 实现求解平方根函数Sqrt(x)  [题目链接](https://leetcode-cn.com/problems/sqrtx/)

题目描述：给定一个非负数x，求解该数字的平方根，如果不是小数，则进行取整处理。例如：Sqrt(8) = 2

思路：当 x > 4 时，其平方根必然小于小于其 x/2，因此可以用二分法来确定，判断 mid-1 和 mid+1是因为结果要进行取整，那么要满足如下等式： $ res^2 \leq x \leq (res+1)^2 $。至于 x <= 4 的情况，可以单独判断列出。

通过的代码如下
```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0:
            return 0
        elif x == 1 or x == 2 or x == 3:
            return 1
        else:
            res = 0
            left = 0
            right = x
            mid = (left + right) // 2
            while (1):
                if mid * mid == x:
                    res = mid
                    break
                elif mid * mid > x:
                    if (mid-1) * (mid-1) <= x:
                        res = mid - 1
                        break
                    else:
                        right = mid - 1
                        mid = (left + right) // 2
                else:
                    if (mid+1) * (mid+1) > x:
                        res = mid
                        break
                    elif (mid+1) * (mid+1) == x:
                        res = mid + 1
                        break
                    else:
                        left = mid + 1
                        mid = (left + right) // 2
            return res
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 按照领域的语言编写代码（Code in the Language of the Domain） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_11/)
每一个领域都有其独特的结构，我们应该按照领域来编写代码。也就是说，设计数据结构时要尽可能的多考虑下相应领域。
- 代码便是设计（Code is Design） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_12/)
写代码是一个创造性的过程，而不是一个机械的过程。就好比盖楼房一样，今天盖楼房的速度远远超过过去，而更多的时间花在了设计建筑上。同样的，今天各种自动化，测试工具使得我们的软件设计可靠性大幅度得到了提升，但是设计不好的代码，想要通过测试工具的测试就不大容易，需要花费更多的时间在改进代码上。
- 代码布局事项（Code Layout Matters） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_13/)
代码布局事项在概念上和代码风格比较类似。代码布局更加强调的是可阅读性，比如合适的缩进，IDE/编辑器中代码的字体、大小、间距以及配色，风格等等。虽然这些项目无关，也没有具体统一的标准，但是它们对一个人来说还是相当重要的，当你使用你所喜欢的布局会在一定程度上提高效率。
- 代码审查（Code Reviews） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_14/)
代码审查是必须的，因为它能提高代码质量同时减少bug。不过，不少人不喜欢代码审查，一个重要的原因便是人们怕受到惩罚。因此不应该对在代码审查发现的问题进行过分的惩罚。代码审查不仅仅是简单地发现、纠正代码中的错误，另一个目的便是建立通用的编码准则。在审查他人代码时要保持谦虚，确保评论有建设性，避开刻薄、直接批评等。
- 用理性写代码（Coding with Reason） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_15/)
前人已经总结了许多好的编码实践，在编写代码应该保持清醒，避免自己出现不符合要求的。具体的一些编码实践如下：避免使用goto语句；避免使用可变的全局变量；每个变量的应具有尽可能小的作用范围；对象默认不可变，而不是可变；变量名、函数名使用简单清晰的命名；函数的功能要尽可能简单，参数要尽可能的少；某一对象提供的对外接口要可能简单，少。

### Tips
Python中字符串方法str.isdecimal()、str.isdigit()、str.isnumeric() 初看很类似，但具体而言还是有一定区别的，具体区别如下：
str.isdecimal()：是否仅为十进制数
str.isdigit()： 是否为小数，上标，下标
str.isnumeric()：是否为小数，下标，上标，普通分数，罗马数字，货币数字
下面是示例代码：
```python
print("'34'.isdecimal() is " + str('34'.isdecimal()))           # True
print("'\u00B2'.isdecimal() is " + str('\u00B2'.isdecimal()))   # False
print("'\u00BC'.isdecimal() is " + str('\u00BC'.isdecimal()))   # False

print("'34'.isdigit() is " + str('34'.isdigit()))               # True
print("'\u00B2'.isdigit() is " + str('\u00B2'.isdigit()))       # True
print("'\u00BC'.isdigit() is " + str('\u00BC'.isdigit()))       # False

print("'34'.isnumeric() is " + str('34'.isnumeric()))           # True
print("'\u00B2'.isnumeric() is " + str('\u00B2'.isnumeric()))   # True
print("'\u00BC'.isnumeric() is " + str('\u00BC'.isnumeric()))   # True
```

### Sharing
Code Review 是很重要的，但是很多时候做的并不好，甚至有些地方干脆没有。我认为 Code Review 就好比学生时代互相检查作业一样，但是由于种种原因，code review很难做好，同时，code review也需要一定水平或水平相似的人来做，试想一个水平较低的人去 Review 水平较高的人的代码，发现其代码中潜在问题的可能性较低。
在 Tips 中，str.isdigit()、str.isnumeric()中的上下标、普通分数，罗马数字，货币数字主要指的是 Unicode 编码，而不是 ASCII 码。