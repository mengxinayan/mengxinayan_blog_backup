标题： ARTS Week 18
分类： ARTS
tags： ARTS
-----------------------------------

Feb 24, 2020 ~ Mar 1, 2020

### Algorithm
Problem 371. Sum of Two Integers（两整数之和）    [题目链接](https://leetcode-cn.com/problems/sum-of-two-integers/)

题目描述：给定两个数字，求两个数字之和。不能使用加法运算

思路为：不能使用加法运算，那么可以考虑使用位运算来实现加法。先观察只有一位数的情况：
```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 0（进位为 1）
```

这个特性符合异或运算，那么可以通过异或运算来实现无进位加法，那么该如何计算进位呢？我们知道，二进制中有逢二进一，可以通过使用与运算得到进位，但是需要额外左移 1 位，因为 `(1 & 1) << 1 = 10`。一直循环此过程，直到进位等于 0

但是，Python 中的整数并不是 32 位，因此需要进行特殊处理，采用 MASK 掩码以保证不会超过32位，利用 MAX_INT 来判断是正数还是负数。

通过的代码如下：
```python
class Solution:
    def getSum(self, a: int, b: int) -> int:
        MASK = 0x100000000
        MAX_INT = 0x7FFFFFFF
        MIN_INT = MAX_INT + 1
        while b != 0:
            carry = (a & b) << 1 
            a = (a ^ b) % MASK
            b = carry % MASK
        if a <= MAX_INT:
            return a
        else:
            return ~((a % MIN_INT) ^ MAX_INT)
```

### Review
本周继续 Review 每个程序员需要知道的 97 件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：

- 使隐形的东西更加可见（Make the Invisible More Visible） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_56/)
为了避免某些潜在的错误，可以使用以下方式来避免：编写单元测试并通过单元测试；使用相关工具管理项目和 bug；使用增量开发的方式

- 使用消息传递提供并行系统的可伸缩性（Message Passing Leads to Better Scalability in Parallel Systems） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_57/)
并发能够显著地提高系统的性能，但是并发中进程间的通信一直是一个问题，文中给出一个建议时使用消息传递，而不是使用共享内存，因为使用共享内存无法保证数据的一致性。

- 给未来的信息（A Message to the Future） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_58/)
当过一段时间后，我们很有可能会无法理解我们当初写的代码，为了以便于未来能够理解，我们需要尽可能地做好完整的注释和文档，以便于未来能很快的理解代码

- 缺少多态的机会（Missing Opportunities for Polymorphism） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_59/)
多态时面向对象的一大特性，对象可以保持接口一致但不同对象执行不同的操作。善用多态可以节省不少工作量，同时可以便于使用者使用。

- 测试人员是您的朋友（News of the Weird: Testers Are Your Friends） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_60/)
大多时候，我们不喜欢测试人员，因为他们总是发现我们错误并告诉我们，像读书时的老师一样。但实际上，我们应该把测试人员当成是我们的朋友，他们帮助我们发现代码中的问题，以便于我们能够改正它，进而避免更大的损失。

### Tip

在 Linux 中，用户调用系统调用时，使用系统调用时传递参数时，参数的值会从用户空间复制到内核空间。主要原因如下：
1. 用户空间程序不能访问内核地址
2. 无法保证用户空间指针指向的虚拟内存页与物理内存页关联

### Share

本周主要是在填上周欠下的坑，虽然花了不少时间，但是还没有填完。。。 :(
