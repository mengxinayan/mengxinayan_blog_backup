标题： ARTS Week 20
分类： ARTS
tags： ARTS
-----------------------------------

Mar 9, 2020 ~ Mar 15, 2020

### Algorithm
Problem 459.Repeated Substring Pattern（重复的子字符串）    [题目链接](https://leetcode-cn.com/problems/repeated-substring-pattern/)

题目描述：给定一个字符串，判断其是否由某些子字符串重复（不存在共用某个字符的情况）组成。例如："abab" 是由 "ab" 字符串重复构成，"aba" 没有重复的字符串，"ababa" 虽然可以分离出两个 "aba" 字符串，但是它们共用了字符 'a'。

思路为：假如一个字符串 s 由 n 个重复的子串 sub 组成，那么 s = sub + ... + sub ，构造一个新字符串 s+s = sub + ... + sub + sub + ... + sub，在里面可以找到 n+1 个字符串 s。举例 s = 'abab' , s + s = 'abababab' 里面可以找到 3 个字符串 s。如果不是由重复的字符串构成，比如 s = 'qwe'，在 s+s = 'qweqwe' 中可以找到两个字符串，我们可以发现，这两个字符串起始位置位于 0 和 len(s) 。因此我们只需要构造 s+s 字符串，如果在 1 到 len(s) - 1 的范围中可以找到字符串 s，那么则可以说明字符串 s 是由重复的子字符串构成。

通过的代码如下
```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        return (s+s).index(s, 1) != len(s)
```

### Review
本周继续 Review 每个程序员需要知道的 97 件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：

- 防止错误（Prevent Errors） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_66/)
错误时用户与系统其余部分之间最关键的交互，用户的不正确输入是导致错误的一大原因，因此需要给用户一定的提示来帮助他们正确输入。此外因为 BUG 也经常会带来错误，因此需要对这些错误进行记录，当出现这种情况后，提示用户重新启动程序即可，没有必要告诉用户错误的原因和详细情况。

- 专业程序员（The Professional Programmer） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_67/)
专业程序员最重要的一个特征就是个人责任感。专业程序员对他们的职业，估计，时间表承诺，错误和技术负责。专业程序员不会将这一责任转移给其他人。

- 将所有内容位于版本控制之下（Put Everything Under Version Control） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_68/)
当项目位于版本控制值夏，你可以跟踪其历史纪录，查看谁写了什么代码，并通过唯一标识符来确定文件或项目版本，同时可以减少开发人员之间的冲突，因为版本控制软件会提醒存在冲突。因此将项目所有资产放置于版本控制之下，除了源代码，包括文档，工具，构建脚本等。可以大幅度降低丢失/损坏磁盘的损失

- 把鼠标放下并远离键盘（Put the Mouse Down and Step Away from the Keyboard） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_69/)
有时候，长时间的工作并不会提高工作效率，相反的，会降低工作效率，如果思考一个问题或解决一个 BUG 耗费了很长时间，你需要把鼠标放下并远离键盘，如果允许，可以出外面走一走，也许过一会儿你就会找到哦呵解决办法

- 阅读代码（Read Code） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_70/)
阅读代码应该多思考思考，当觉得某些代码难以阅读时思考什么原因导致代码难以阅读，同样地，当觉得某些代码易于阅读时思考什么原因导致代码易于阅读。当编写代码时，应该尽可能保证自己的代码易于阅读。

### Tip

JavaScript 默认的排序方法 sort() 方法比较奇怪，需要自己来进行更新

```js
// 看上去正常的结果:
['Google', 'Apple', 'Microsoft'].sort(); // ['Apple', 'Google', 'Microsoft'];
// 按照 ASCII 码值大小进行排列
['Google', 'apple', 'Microsoft'].sort(); // ['Google', 'Microsoft", 'apple']

// 无法理解的结果:
[11,22,10,20,1,2].sort(); // [1, 10, 11, 2, 20, 22]
```

最后对数字的排序为什么得到了与平常不同的结果，是因为 JavaScript 是直接按照数字进行排序！幸运的是，在 JavaScript 中，sort 是一个高阶函数，可以用程序员重写，可以设定自己的排序规则，举例如下：

```js
'use strict';
var arr = [11,22,10,20,1,2];

// 从小到大排序
arr.sort(function (x, y) {
    if (x < y) {
        return -1;
    }
    if (x > y) {
        return 1;
    }
    return 0;
});
console.log(arr); // [1, 2, 10, 11, 20, 22]

// 从大到小排序
arr.sort(function (x, y) {
    if (x < y) {
        return 1;
    }
    if (x > y) {
        return -1;
    }
    return 0;
}); 
console.log(arr); // [22, 20, 11, 10, 2, 1]
```

参考资料：1. 廖学峰大佬的 JavaScript 教程中的 sort 章节，[链接](https://www.liaoxuefeng.com/wiki/1022910821149312/1024328479098336)

### Share

本周如期完成了工作，开始进入了下一阶段的工作。现在还需要先去补充学习一定的知识。
