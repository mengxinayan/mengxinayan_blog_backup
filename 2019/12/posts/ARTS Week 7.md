标题： ARTS Week 7
分类： ARTS
tags： ARTS
-----------------------------------

Dec 9, 2019 ~ Dec 15, 2019
### Algorithm
Problem 38.Count And Say 外观数列 [题目链接](https://leetcode-cn.com/problems/count-and-say/)

题目描述： *外观数列* 是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。前六项及其说明如下：
1. 1        // base
2. 11       // 描述[1]：1个1 -> 11
3. 21       // 描述[2]：2个1 -> 21
4. 1211     // 描述[3]：1个2,1个1 -> 1211
5. 111221   // 描述[4]：1个1,1个2,2个1 -> 111221
6. 312211   // 描述[5]：3个1,2个2,1个1 -> 312211

解题思路：1是一个初始情况，需要单独处理。对字符串进行遍历，先获得字符串中的开头的数字，然后判断下一个数字是否与前面数字相同，若相同，则计数加一。若不相同，则通过 res = res + str(num) + tmp 语句更新结果，同时将数字替换为当前的数字

通过的代码如下：
```python
class Solution:
    def countAndSay(self, n: int) -> str:

        def read(string: str) -> str:
            tmp = ''
            num = 0
            res = ''
            for i in range(0, len(string)):
                if string[i] == tmp:
                    num += 1
                else:
                    if i != 0:
                        res = res + str(num) + tmp
                    tmp = string[i]
                    num = 1
            res = res + str(num) + tmp
            return res

        res = '1'
        for i in range(n-1):
            res = read(res)
        return res
```

### Review
接下来的几周，我准备简单 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。初步计划为每周5个小内容。下面是本周的5个小内容：
- 谨慎行动（Act with Prudence） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_01/)
无论计划表看起来时间多么充裕，但总是无法避免遇到问题。当你在“尽快地做”和“做正确的事”之间选择“尽快地做”时，它可能会为以后带来隐患，一般称其为技术债务。技术债务和贷款一样，虽然你可以从短期受益，但利息需要尽快还清。利息包括潜在的bug，不完整的测试案例，等等。如果不及时偿还利息，那么问题将会越来越多，随着问题的增多，想要修正某一问题将会变得困难，就好比利滚利一样，最后无力偿还只能宣布破产（软件的生命结束）。
避免出现上述情况的办法就是尽快处理问题，避免问题的积累。当然，更好的办法便是谨慎行动，减少可能会带来的问题。
- 使用函数式编程原则（Apply Functional Programming Principles） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_02/)
函数时编程有利于提高代码的质量，因为只要函数一旦确定，那么每一个输入的情况，其输出结果是可以预测的。函数的功能越单一，可以减少依赖，同时方便进行测试和改进。函数式编程的一大优点便是避免了面向对象中那复杂的依赖关系，以及成员之间可能会发生的变化。
当然，面向对象也有其相应的优点，比如面向对象可以有效处理业务规则的复杂性。函数式编程与面向对象编程就好比同一事物的阴阳两面。
- 多试着问一问自己“用户会怎么做” （Ask "What Would the User Do?" (You Are not the User)） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_03/)
我们总是错误地认为他人遇到问题的思考方式、思考过程会和自己一样。但事实上并非如此，每个人的差异巨大，当遇到问题时的处理方式也千差万别。因此，为了保证软件对用户的可用性，我们需要从用户的角度来思考，想清楚他们需要什么，但把自己想象成用户并不容易，更好的方式去问用户，了解其内心的想法。不幸的是，很多的用户的表达能力不是很好，他们很难用准确的语言来描述他们需要什么，因此需要一定的沟通技巧来引导用户，或者观察用户的行为以推测他们的需求。
- 利用自动化工具检查编码标准（Automate Your Coding Standard）[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_04/)
为整个项目/团队设置统一的编码标准有利于管理。这些编码标准包括缩进、变量/函数等的命名以及其他。为了能有效地控制编码标准，需要利用一些自动化工具，可以进行监测，发现不符合规范的代码，甚至可以给出修改建议等
- 简单便是美（Beauty Is in Simplicity） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_05/)
我们在代码中经常有对可读性、可维护性、可开发速度以及追求美的需求。那么什么样的代码是美的呢，柏拉图曾说过美源自简约。在简单代码中，每个单独的模块保持简单，并承担简单的任务，系统各个模块联系也同样简单。代码的可读性、可维护性比较高，同时再开发增加新的模块时也比较容易。

### Tips
gcc编译多线程的程序需要增加 -lpthread 选项 或者 -pthread 选项。

### Sharing
在 Review 部分，简单的讲述了5个，有一些内容是我之前也清楚的，比如考虑用户，良好的编码规范。也有一些是有所耳闻的，比如谨慎行动，简单便是美。还有一些是之前从未了解过的，比如使用函数式编程，自己之前也从未接触过函数式编程，所以即使读完以后也不甚了解，在网上查阅资料后，才知道 Haskell 是典型的函数式语言，希望自己能抽空来学习一下。