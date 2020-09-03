标题： ARTS Week 17
分类： ARTS
tags： ARTS
-----------------------------------

Feb 17, 2020 ~ Feb 23, 2020
### Algorithm
Problem 205.Isomorphic Strings（同构字符串）    [题目链接](https://leetcode-cn.com/problems/isomorphic-strings/)

题目描述：给定两个字符串 s 和 t，判断是否可以通过字符替换从 s 得到 t。顺序不可以改变，同时不允许两个字符映射到同一个字符，但允许一个字符映射到它自身。举例如下：
Input: s = "egg", t = "add"
Output: true

Input: s = "foo", t = "bar"
Output: false

思路为：可以通过字典来建立映射关系。因为不允许两个字符映射到同一个字符，因此需要检查将要映射的字符是否已经出现在字典的 value 中。总结下来便是：若键值已出现在字典的 key 中，那么检查是否满足映射关系，若不满足，则为 False。满足继续遍历；若键值未出现在字典的 key 中，检查将要映射的字符是否已经出现在字典的 value 中，若出现，则为 False，若没有则更新现有的映射关系。直到遍历结束，则为 True

通过的代码如下
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        char_map = {}
        res = True
        for i in range(len(s)):
            if (s[i] not in char_map) and (t[i] not in char_map.values()):
                char_map[s[i]] = t[i]
            elif (s[i] not in char_map) and (t[i] in char_map.values()):
                res = False
                break
            else:
                if char_map[s[i]] != t[i]:
                    res = False
                    break
        return res
```

### Review
本周继续 Review 每个程序员需要知道的 97 件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：

- 学会如何说 “Hello World”（Learn to Say "Hello, World"） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_51/)
当我们在学习新的编程语言或者新的外语时，都需要学习最基本的内容，便是 "Hello World"。

- 让您的项目自己说话（Let Your Project Speak for Itself） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_52/)
需要给项目一个声音。以便于项目出现问题时，可以通过电子邮件或即时消息传递来完成，通知开发人员知道最新情况，同时，可以根据项目的紧急情况设置不同的等级，就好比交通信号灯有红灯和黄灯。

- 链接器不是一个神奇的程序（The Linker Is not a Magical Program） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_53/)
很多人在将源代码通过编译链接变成可执行文件的过程时，经常遇到某些警告，比如：链接器说一个变量被多次定义，链接器说一个变量未被定义。忽略这些警告是不明智的，虽然链接器有可能会解决这些问题，但并不是所有警告都能解决，更好的办法是自己去解决这些问题。

- 临时解决方案的寿命（The Longevity of Interim Solutions） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_54/)
通常为了快速解决一些眼前的问题，可能需要开发一个临时工具/方案来应急解决。但是，我们仍需要真正的方案去解决这个问题，如果不及时解决，那么临时解决方案会越来越多，进而导致项目的内部复杂性增加，可维护性下降。因此，当我们使用了临时解决方案后，应该尽快采用正式解决方案来取代它，而不是一直保留它。

- 使接口易于正确使用（Make Interfaces Easy to Use Correctly and Hard to Use Incorrectly） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_55/)
接口开发是软件开发中最常见的任务之一，无论是用户接口，还是功能接口，亦或是类接口、库接口等。好的接口是易于使用者使用和修改。总之，一个原则便是：存在接口是为了方便用户，而不是接口的实现者。

### Tip

C/C++ 中 static 作为修饰词修饰函数的作用：避免冲突限定作用域，一个函数只可以在一个文件中出现。

### Share

本周花了不少时间在折腾某些基础设施和无聊的事，因为不太熟悉，消耗了太多时间。原来真正打算做的事结果并没有做了多少。
