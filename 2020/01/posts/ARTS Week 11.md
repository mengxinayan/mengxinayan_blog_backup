标题： ARTS Week 11
分类： ARTS
tags： ARTS
-----------------------------------

Jan 6, 2020 ~ Jan 12, 2020
### Algorithm
Problem 108 Convert Sorted Array to Binary Search Tree (将有序数组转化为二叉搜索树)  [题目链接](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

题目描述：给定一个有序数组，将其转换为一个高度平衡的二叉搜索树。高度平衡：对于树中任一结点，其左子树和右子树的高度不大于1。二叉搜索树：对于树中任一结点，其左子树所有结点的值小于等于该结点的值，其右子树所有结点的值大于等于该结点的值。例如给定数组为 [-10,-3,0,5,9]，得到的高度平衡的二叉搜索树如下：
```
      0
     / \
   -3   9
   /   /
 -10  5
```
思路为：因为题目要求高度平衡，那么说明左右子树结点数目应该相近，同时要求是高度平衡和二叉搜索树都是递归的定义，且给定的是一个有序数组，不难想到使用递归。递归的初始条件便是：数组中没有元素或者只有一个元素，没有元素返回 None 即可，只有一个元素，则用该元素的值构建一个树结点即可。若多于一个元素，可以用 nums[len(nums)//2] 构建根节点，之后用 nums[0: len(nums)//2] 和 nums[len(nums)//2+1: len(nums)] 分别构建左右子树。

通过的代码如下
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if len(nums) == 0:
            return None
        if len(nums) == 1:
            node = TreeNode(nums[0])
            return node
        node = TreeNode(nums[len(nums)//2])
        node.left = self.sortedArrayToBST(nums[0: len(nums)//2])
        node.right =  self.sortedArrayToBST(nums[len(nums)//2+1: len(nums)])
        return node
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 区分业务异常和技术异常（Distinguish Business Exceptions from Technical） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_21/)
技术异常取决有编程语言本身，比如大多数语言在访问超出数组索引的元素时，会抛出一个异常来告诉你出现了错误。而业务异常是根据业务规则确定的，比如，银行账户只有100元，但想要取出200元时就会产生的一个异常。无论是技术异常还是业务异常我们都需要正确的处理它。

- 刻意练习（Do Lots of Deliberate Practice） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_22/)
刻意练习不只是单单执行任务，完成任务。而是有意识的练习一提高执行任务的能力。刻意练习意味着重复，多次重复一达到掌握的程度。刻意练习那些已经掌握的东西毫无意义，刻意练习应该去练习那些不擅长，不熟悉的东西。

- 领域特定语言（Domain-Specific Languages） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_23/)
每一个领域都有其特定的术语，用于描述该领域特有的事物。领域特定语言（DSL）一般分为内部和外部：内部DSL是通用编程语言编写而成的，内部DSL封装了现有的API，库和业务代码，并且对外部提供必要的接口。外部DSL是语言的文本或图形表达，其可以包括词法分析器，语法分析器等。其中将外部DSL采用XML、Json等格式也很常见。

- 不要害怕犯错误（Don't Be Afraid to Break Things） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_24/)
无论一个多么有经验的人都可能会犯错误，通过犯错误进而改正错误有助于提高自己。当然犯错误也可能会带来问题，比如受到批评、惩罚等，所以可能存在害怕出错的心理。在软件开发过程中，有一个比较好的减少错误的办法便是，一次只进行小量的改动，而立马进行测试，通过这样的小而快的迭代，可以避免犯下大的错误。

- 不要对你的临时数据不满意（Don't Be Cute with Your Test Data） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_25/)
在代码中编写任何文本时（无论是注释，日志，对话框还是测试数据），请始终问问自己，如果公开，它将如何显示。它将全面保存一些信息。

### Tips
Python中字符串方法str.ljust()，str.rjust()，str.center()，str.strip()，str.lstrip()，str.rstrip()的功能分别如下：
- str.ljust() ：填充字符串，让其左对齐。默认用空格填充
- str.rjust() ：填充字符串，让其右对齐。默认用空格填充
- str.center()：填充字符串，让其居中。默认用空格填充
- str.strip() ：截掉字符串两边的指定字符，默认是空白字符集合 
- str.lstrip()：截掉字符串左边的指定字符，默认是空白字符集合
- str.rstrip()：截掉字符串右边的指定字符，默认是空白字符集合
空白字符集合为：{ ' ', '\t', '\n', '\v', '\f', '\r' }
示例如下：
```python
s0 = 'hello'
s11 = s0.ljust(10)
s12 = s0.ljust(10,'!')
s21 = s0.rjust(10)
s22 = s0.rjust(10,'!')
s31 = s0.center(10)
s32 = s0.center(10,'!')

print('s0 = ',s0)
print('s11 = ',s11)
print('s12 = ',s12)
print('s21 = ',s21)
print('s22 = ',s22)
print('s31 = ',s31)
print('s32 = ',s32)

print('s12.lstrip() = ',s12.lstrip('!'))
print('s12.rstrip() = ',s12.rstrip('!'))
print('s22.lstrip() = ',s22.lstrip('!'))
print('s22.rstrip() = ',s22.rstrip('!'))
print('s32.strip() = ',s32.strip('!'))
print('s32.strip() = ',s32.strip())

'''
输出结果如下：
s0 =  hello
s11 =  hello     
s12 =  hello!!!!!
s21 =       hello
s22 =  !!!!!hello
s31 =    hello   
s32 =  !!hello!!!
s12.lstrip() =  hello!!!!!
s12.rstrip() =  hello
s22.lstrip() =  hello
s22.rstrip() =  !!!!!hello
s32.strip() =  hello
s32.strip() =  !!hello!!!
'''
```

### Sharing
在 Review 部分中，提到技术异常和业务异常的区别，作为程序员，找到的技术异常比业务异常容易不少，但是业务异常同样值得关注，如果不慎就会带来巨大的损失。