标题： ARTS Week 16
分类： ARTS
tags： ARTS
-----------------------------------

ARTS Week 16: Feb 10, 2020 ~ Feb 16, 2020
### Algorithm
Problem 190.Reverse Bits（颠倒二进制位）    [题目链接](https://leetcode-cn.com/problems/reverse-bits/)

题目描述：给定一个 32 bits 的二进制数，输出其逆序的二进制数。注：输入和输出的整数类型均为 32 位无符号整数。举例如下：
输入: 00000010100101000001111010011100
输出: 00111001011110000010100101000000

思路为：自然产生的最简单的思路便是将这 32 个数放在一个列表中，然后调用 list.reverse() 方法，但仔细一想，这样的方法效率很低，会花费大量的用于整数和二进制数的转换上。我们可以换一个思路，可以把结果设定一个值为空的数字，每次从输入中提取一个数字，然后将这个数字送入结果中。我们设定一个 res = 0，每次将其左移一位，那么如何获取输入最后一位是0还是1呢，我们可以使用与运算，通过观察可以发现，数字末尾为1时与数字1进行与运算结果仍为1，数字末尾为0时与数字1进行与运算结果仍为0。最后将输入数字右移一位即可。

通过的代码如下
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        for i in range(32):
            res = res << 1
            res += (n & 1)
            n = n >> 1
        return res
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：

- 知道你的极限（Know Your Limits） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_46/)
你的资源有限，只有那么多的时间和金钱来完成工作。此外，资源还包括硬件资源，比如 CPU，内存等。时间和金钱是软件工程、项目经理应该考虑的事。程序员更应该考虑一个方法的时间复杂度和空间复杂度。比如线性搜索需要 O(n)，二分查找只需要 O(log(n)) 复杂度。同样的，容量和速度的差异也值得注意，比如 CPU 中的寄存器，cache，RAM，硬盘等，其容量和访问速度成反比。

- 了解你的下一次提交（Know Your Next Commit） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_47/)
了解你的下一次提交便是你需要将你的目标细化，比如在一定时间内重构某一函数，增加新的函数或者为某一函数编写单元测试等。如果在时间内无法完成任务，则需要重新将任务划分为更小的任务，或者是求助他人/寻得合作。

- 大型内部有联系的数据属于数据库（Large Interconnected Data Belongs to a Database） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_48/)
如何您的应用要处理大量的，持久的，相互有联系的数据元素，你需要将这些数据存储在关系型数据库中。你可以简单使用 SQL 语句来实现对数据的增删查改，而无需编写复杂的代码。请记住：虽然数据库使程序员变得轻松，但是 SQL 语句的书写就跟算法设计一样，不同的 SQL 语句执行效率也是不同的。

- 学习外语（Learn Foreign Languages） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_49/)
虽然程序员更多的时候再和计算机打交道，但是仍无法避免要与人进行沟通。查理曼大帝曾说到：知道另一种语言就是拥有另一种灵魂。尤其对咱们中国程序员来说更是如此，中文资料虽然也有很多，但很多先进/前沿/时髦的技术都存在于英文中，这些是没有中文的。此外，很多中文资料都是他人翻译过的，并不是一手的，信息会有一定的损失。

- 学会估算（Learn to Estimate） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_50/)
作为程序员，你需要能够为你的经理，同事和用户提供预计完成任务的时间，以便他们可以合理地安排他们的计划。为了能够进行良好的估算，学习一些估算技术显然很重要。估计可以示为一种目标或承诺，错误地估计可能会带来无法避免的损失，尤其当实际情况比你估计的更庞大时。

此外，分享一篇我在 Linux 中国翻译的文章：[检查 Linux 中内存使用情况的 8 条命令](https://linux.cn/article-11870-1.html)

### Tip
分享一篇我写的另一篇文章，[C/C++ 语言宏定义函数编写时 do-while 的妙用和一些注意事项]()

### Share
前一段日子花了很长时间来填之前欠下的 ARTS 的坑，本周终于完成了落下的内容，并将内容发表。就跟每个程序员需要知道的 97 件事中写到的，不要留下技术债，这些内容也可以认为是一种债务，如果我不及时、尽快地将欠下的内容还清，那么将会越积越多，最后只好放弃或者重新开始，这完全可以称得上是半途而废了。此外，我还发现当初写得一篇关于如何安装 Spacemacs 文章浏览量明显更高，因此我决定以后尽可能写更多的涉及到具体技术的文章。
