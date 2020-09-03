标题： ARTS Week 8
分类： ARTS
tags： ARTS
-----------------------------------

Dec 16, 2019 ~ Dec 22, 2019
### Algorithm
Problem 53 Maximum Subarray 最大子数组  [题目链接](https://leetcode-cn.com/problems/maximum-subarray/)

题目描述：给定一个数组，在所有连续的子数组中，求得其中的最大值，举例如下:
数组：[-2,1,-3,4,-1,2,1,-5,4]
返回结果：6， 子数组 [4, -1, 2, 1] 的和最大

思路：该题目有多种可以解决思路。比如分治法，动态规划，贪心法。本次为了方便理解，采用贪心法。贪心法的贪心策略是在某个位置的一个数与其下一个数的和 和 下一个数 中，选择更大的，即 currsum = max(currsum+nums[i], nums[i]) 。若想求得数组中的最大子数组，只需要把每个位置的最大和进行比较，便可以得到最大子数组和，即 maxsum = max(maxsum, currsum)

通过的代码如下
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxsum = currsum = nums[0]
        for i in range(1, len(nums)):
            currsum = max(currsum+nums[i], nums[i])
            maxsum = max(maxsum, currsum)
        return maxsum
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 重构之前（Before You Refactor）  [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_06/)
重构的最佳方法是查看现有代码，从编写针对现有代码的测试开始，这样有助于了解到现有代码的优点和缺点。从而继承优点，避开缺点。重构代码要避免重写所有代码，要尽可能地复用已经有的代码，因为他们已经通过了测试，可以对已有代码进行增量修改。如果必须要编写新代码，那么要保证新代码必须能通过之前的测试。此外，不应该因个人喜好而去重构某些代码。
- 当心共享（Beware the Share） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_07/)
虽然某些地方需要的代码功能很接近，但是因为上下文，以及具体的需求，业务过程不同。贸然的重用代码可能会带来某些难以解决的问题。所以，当重用代码时尽量考虑下具体环境，一旦重用不当，带来的不是便捷性，而是增加了隐患。
- 童子军规则（The Boy Scout Rule） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_08/)
童子军有这样一条规则：“离开营地时要比发现它时干净”。同样地，我们在代码中发现一个不太好的地方后，尽可能帮忙改正。不一定要是重要的问题或者bug之类，一些小的问题也同样值得改进，比如 重新命名下函数中的变量名，将一个长函数拆分为两个或多个函数等等，这样都可以帮助整个项目向好的方向发展。
- 在指责其他之前先检查自己的代码（Check Your Code First before Looking to Blame Others） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_09/)
我们经常遇到这样情况，“为什么我的代码在我本地就跑得好好地，在别的电脑上就不能运行or错误运行，这一定是环境配置不正确，或者编译器/解释器/框架版本的原因，或者干脆是多运行几次，也许有一次能正常运行”。在遇到这些情况时，我们应该首先去检查自己的代码是否存在问题，而不是去抱怨/指责环境，其他客观问题。事实上，大部分这种情况出现根源还是在代码本身
- 谨慎选择工具（Choose Your Tools with Care） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_10/)
现如今，Web 上许多可用的工具用来帮助你构建某些功能、模块。但是，不同工具可以利用了不同的依赖（比如：基础结构，控制模型，数据模型，通信协议），而在这些内容可能存在某些冲突。不同的工具具有不同的生命周期，一些生命周期长的工具，通常也比较复杂，你需要事先进行配置。此外，如果你选择自由软件，可能你的产品会受到其约束（例如GPL协议），如果你选择商业软件，可能你会发现开销很大。因此，选择工具时需要谨慎，尽可能少的，选择有用的工具。

### Tips
Python中检查字符串中是否由某些字符组成的函数有很多，下面是一些详细的解释：
str.islower()、str.isupper()、str.istitle()：这三个方法很类似，其结果为 True 的有两个条件，其一字符串中至少有一个字符是可以有大小写的，这个条件三个方法是相同的。不同的是第二个条件，
- str.islower()：指的是所有这些可以有大小写的字符均为小写
- str.isupper()：指的是所有这些可以有大小写的字符均为大写
- str.istitle()：指的是字符串中的所有单词都是标题化的（即首字符有大小写字符的大写字符，其余字符中有大小写字符的均为小写字符）。
具体举例如下：
```python
print('123')
print('123.islower() is ' + str('123'.islower())) # False
print('123.isupper() is ' + str('123'.isupper())) # False
print('123.istitle() is ' + str('123'.istitle())) # False

print('1q@#')
print('1q@#.islower() is ' + str('1q@#'.islower())) # True
print('1q@#.isupper() is ' + str('1q@#'.isupper())) # False
print('1q@#.istitle() is ' + str('1q@#'.istitle())) # False

print('QAQ')
print('QAQ.islower() is ' + str('QAQ'.islower())) # False
print('QAQ.isupper() is ' + str('QAQ'.isupper())) # True
print('QAQ.istitle() is ' + str('QAQ'.istitle())) # False

print('Qaq')
print('Qaq.islower() is ' + str('Qaq'.islower())) # False
print('Qaq.isupper() is ' + str('Qaq'.isupper())) # False
print('Qaq.istitle() is ' + str('Qaq'.istitle())) # True

print('Q123-q.istitle() is ' + str('Q123-q'.istitle())) # False
print('Q123-Q.istitle() is ' + str('Q123-Q'.istitle())) # True
```

str.isspace()，str.isalpha()，str.isalnum()：这三个方法很接近，其含义分别为：
- str.isspace()：表示字符串中至少有一个字符，且所有字符均在此字符集合中 { ' ', '\t', '\n', '\v', '\f', '\r' }，则结果为 True
- str.isalpha()：表示字符串中至少有一个字符，且所有字符均字母字符，则结果为 True
- str.isalnum()：表示字符串中至少有一个字符，且所有字符均字母或数字字符，则结果为 True。
举例如下：
```python
print("'qwe asd'.isspace() is " + str('qwe asd'.isspace()))         # False
print("''.isspace() is " + str(''.isspace()))                       # False
print("' \t\n\v\f\r'.isspace() is " + str(' \t\n\v\f\r'.isspace())) # True

print("''.isalpha() is " + str(''.isalpha()))                       # False
print("'qwe'.isalpha() is " + str('qwe'.isalpha()))                 # True
print("'123qwe'.isalpha() is " + str('123qwe'.isalpha()))           # False

print("''.isalnum() is " + str(''.isalnum()))                       # False
print("'qwe'.isalnum() is " + str('qwe'.isalnum()))                 # True
print("'123qwe'.isalnum() is " + str('123qwe'.isalnum()))           # True
```
最后，还剩下三个类似于上面六个的函数，分别为str.isdecimal()、str.isdigit()、str.isnumeric()。它们之间的区别我现在还没有太清楚，等我清楚后再记录下来。更新：它们三者之间的区别我将其记录在了下一周的ARTS中，文章链接如下：ARTS Week 9

### Sharing
在 Review 部分中，提到谨慎选择工具，我觉得很不错。很多人喜欢用现有的库来完成某一任务，如果你的软件仅仅是像学生时代交作业时检查通过后便不再维护，那么用这些库来完成任务是可以的。但是，如果你的软件需要长时间维护，那么用现有的库则需要谨慎。具体优缺点见 Review 部分。