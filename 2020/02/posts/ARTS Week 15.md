标题： ARTS Week 15
分类： ARTS
tags： ARTS
-----------------------------------

Feb 3, 2020 ~ Feb 9, 2020
### Algorithm
Problem 172.Factorial Trailing Zeroes（阶乘末尾的0）    [题目链接](https://leetcode-cn.com/problems/factorial-trailing-zeroes/)

题目描述：给定一个整数n，求 n! 的末尾0的个数

思路为：因为 2 × 5 = 10，因此只要求得 n! 中因数 2 和 5 个数中的较小值，显然，因数为 5 的个数比因数为 2 的个数少。因为$ n! = 1*2*...*(n-1)*n $，那么也就是求 1,2,...,n-1,n 这一列数中因数5的个数。我们发现只有 5, 10, 15, ... 的因数中才含有 5。因此我们容易想到通过计算 n//5 来求得因数等于5的个数，但这并没有全部算进去，因为像 25,50,125,625 这些数字不只含有一个因数5。因此，正确的求解公式如下：
$$ n! = \left \lfloor \frac{n}{5} \right \rfloor + \left \lfloor \frac{n}{5*5} \right \rfloor + \cdots + \left \lfloor \frac{n}{5 ^ {n-1}} \right \rfloor + \left \lfloor \frac{n}{5^n} \right \rfloor + \cdots = \left \lfloor \frac{n}{5} \right \rfloor + \cdots + \left \lfloor \frac{n}{5^k} \right \rfloor , 5^k \leq n < 5^{k+1} $$

通过的代码如下：
```python
class Solution:
    def trailingZeroes(self, n: int) -> int:
        res = 0
        tmp = 5
        while n >= tmp:
            res += (n // tmp)
            tmp *= 5
        return res
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 进程间通信影响应用程序响应时间（Inter-Process Communication Affects Application Response Time） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_41/)
响应时间是一个软件可用性的重要衡量标准，响应时间太久很容易带来用户的反感。而占据响应时间最多的便是进程间通信（IPC），IPC太慢或者IPC个数太多都会影响响应时间。优化方法有如下三种：1）优化进程间通信的速度，2）减少不必要进程间通信个数，3）缓存以前的进程间通信结果

- 保持构建清洁（Keep the Build Clean） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_42/)
随着项目的增长，警告会越来越多，它们之间的关系也越来越复杂，想找到自己的所需要的警告也很难。因此在出现警告后应该尽快处理警告，避免警告越积累越多，警告也是代码卫生的重要的组成部分。

- 知道如何使用命令行工具（Know How to Use Command-line Tools） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_43/)
现如今，有许多集成开发环境（IDE）可供使用，IDE有许多优点，但同样也有缺点，其屏蔽了底层细节导致你无法准确知道发生了什么。而使用命令行构建工具，你可以知道构建可执行文件的所有步骤（编译，链接）。此外，命令行工具中有些一个图形化界面更加强大，比如 grep 和 sed。当然，这并不是建议你放弃 IDE 而完全去使用命令行。

- 学会至少两种编程语言（Know Well More than Two Programming Languages） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_44/)
虽然现在有些语言相当流行，比如 Java，C/C++，Python。但是仅仅学习其中一种是远远不够的，你应该多学习一种语言，不同语言有着不同的差异，学习新的语言并明白它与已经学会的语言之间的区别，在对比二者的同时，互相取长补短，能获得更深刻的理解。

- 了解你的IDE（Know Your IDE） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_45/)
现代IDE使用起来十分方便，但是如果你并不熟练它，使用它的效率并不高。学习 IDE 的第一步便是了解其键盘快捷键。但是某些 IDE 寿命并不长，他们使用的快捷键也可能在将来无法使用，因此去学习那些命令行工具吧，比如 grep(1974年出现) sed(1974年出现) awk(1977年出现) 等。它们存在了几十年，并仍将存在。

### Tips
在 Python2 中，检查一个值是否为一个字典中的键中可以使用dict.has_key() 方法，而在 Python3 中，字典中没有该方法。无论 Python2 还是 Python3 都可以使用 in 关键字来进行检查某个键值是否存在。示例代码如下：
```python
Python 2.7.14 (default, Oct 12 2017, 15:50:02) [GCC] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> a = {1:'a', 2:'b'}
>>> a
{1: 'a', 2: 'b'}
>>> a.has_key(1)
True
>>> 1 in a
True

Python 3.6.10 (default, Jan 16 2020, 09:12:04) [GCC] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> a = {1:'a', 2:'b'}
>>> a
{1: 'a', 2: 'b'}
>>> a.has_key(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'dict' object has no attribute 'has_key'
>>> 1 in a
True
```

### Sharing
命令行工具是非常有用且强大的，它们通过提供许多的选项来使其具有强大的功能，有兴趣可以去看看 grep apt rpm 等命令的手册，它们都具有很多的选项。不过，正是由于其选项复杂，当不熟悉时，命令行使用起来没有 GUI 工具方便。GUI 工具也可以实现复杂的功能，但是很多使用 GUI 工具的人对其复杂的功能并不熟悉，就拿我个人而言，虽然在使用 IDEA，Visual Studio。但是，自己对这些工具并不熟悉，有一些功能总是在上网查询后才知道如何使用，并且一段时间不使用的话就很容易忘记了。