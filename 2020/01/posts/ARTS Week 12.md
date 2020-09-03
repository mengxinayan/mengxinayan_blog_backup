标题： ARTS Week 12
分类： ARTS
tags： ARTS
-----------------------------------

Jan 13, 2020 ~ Jan 19, 2020
### Algorithm
Problem 112. Path Sum (路径总和)    [题目链接](https://leetcode-cn.com/problems/path-sum/)

题目描述：给定一棵二叉树和一个值 sum ，检查二叉树是否存在根到叶子路径之和等与 sum 的路径，若存在，则返回 true，反之返回 false。例如，sum = 22，二叉树如下：
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```
返回结果 true，因为 5->4->11->2

思路为：树的遍历要使用递归，sum同时要保持更新，比如上面的例子中，使用了根节点后，sum = 22 - 5 = 17，需要对结点为空结点和叶子结点进行特殊处理。

通过的代码如下
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        if root == None:
            return False
        elif root != None and root.left == None and root.right == None:
            return (sum == root.val)
        else:
            return (self.hasPathSum(root.left, sum-root.val)) or (self.hasPathSum(root.right, sum-root.val))
```
### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 不要忽略错误（Don't Ignore that Error!） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_26/)
异常是一个很好的指示和处理错误的方式，但是很多代码中仅仅是捕捉到异常而不去处理异常，比如下面的代码
```
try {
    // ...do something...
}
catch (...) {} // ignore errors
```
忽略错误可能会导致一些严重的后果：比如产生难以发现的错误，利用错误来侵入、破坏软件。因此，我们需要对错误进行处理，而不是忽略它。

- 不要仅仅学习语言，而要了解其文化（Don't Just Learn the Language, Understand its Culture） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_27/)
编程语言有许多，它们都有着独特的特点和适用的条件。单单学习语言可能会无法理解某一些语言，尤其是一些差别比较大的语言时。比如一直学习并使用 Java，然后去学习 Haskell 时，可能会对函数式编程产生疑惑，此时应该去了解下函数式编程的文化，比如产生的背景，原因，目的，生态等。

- 不要将程序钉在直立位置（Don't Nail Your Program into the Upright Position） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_28/)
应该尽可能是的使用异常来妥善处理错误，而不是直接将错误抛给用户。就好比 UI 设计中有一条规则，永远不要让用户看到错误报告，而是好像解决了问题。因为直接弹出的错误会给用户带来不好印象，同时大部分用户即使知道了错误原因也并知道如何改正它。

- 不要依赖“魔术发生”（Don't Reply on "Magic Happens Here"） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_29/)
很多情况下，即使你不了解具体情况，程序仍可以正常运行，我们称其为“魔法”。比如，程序有内存泄漏的错误，但是每次泄漏的内存都很少，也许程序一直运行十几个甚至几十个小时也不会出现问题，但是终有一刻内存被耗尽了，问题出现了。

- 不要重复自己（Don't Repeat Yourself） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_30/)
不要重复自己（DRY）是所有编程中最基本的原则之一，其中包含三个子观点。1）复制是浪费：每一行代码都必须得到维护，不必要的复制会使代码库膨胀，同时给系统增加了不必要的复杂性。2）流程重复要求自动化：开发过程中有不少过程是重复的，比如测试，如果手动完成则需要增加许多不必要的劳动。3）逻辑重复要求抽象：逻辑重复可以用复制粘贴 if-else 或者switch-case 来进行检测，更好的方式是利用设计模式来避免，比如工厂方法。

### Tips
Python 中字符与 ASCII 码值的转换：ord()函数是将字符转换为 ASCII 码值，chr()函数是将 ASCII 码值转换为字符，举例如下：
```python
print("ord('H') = ",ord('H')) # ord('H') =  72
print("chr(77) = ",chr(77))   # chr(77) =  M
```

### Sharing
在 Review 部分中提到的不要将程序钉在直立位置（Don't Nail Your Program into the Upright Position），我认为是一个很取巧的办法，这样做有好有坏，不管是仅仅报告出现错误，还是具体的错误原因。我觉得对用户的影响是一样的，好的办法是报告一个简略的错误，不想具体了解的用户进需要知道发生错误即可，想具体了解错误的用户可以查看详细错误。