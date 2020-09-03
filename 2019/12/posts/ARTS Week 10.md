标题： ARTS Week 10
分类： ARTS
tags： ARTS
-----------------------------------

Dec 30, 2019 ~ Jan 5, 2020
### Algorithm
Problem 88 Merge Sorted Array (合并两个有序数组)  [题目链接](https://leetcode-cn.com/problems/merge-sorted-array/)

题目描述：给定两个有序数组 nums1，nums2，其长度分别为m，n。假设 nums1 有足够的空间(m+n)，将 nums2 中的数组添加到已有的 nums1 数组中。不返回任何值。举例如下：
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3
合并后的 nums1 = [1,2,2,3,5,6]

思路：在我做题时发现，实际输入的 nums1 后面会多 n 个0，因此要先去掉这些多余的0。而后便是从头开始遍历 nums1 和 nums2，若 nums2 某位置的元素小于等于 nums1 某位置的元素，那么则把 nums2 的相应元素插入到 nums1 的位置前面，若 nums2 某位置的元素大于 nums1 某位置的元素，那么 nums1 向前前进一个元素。最后，判断若是 nums1 先到达了末尾，那么把剩余的 nums2 元素都插入到 nums1 中。

通过的代码如下
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        if n == 0:
            pass
        elif m == 0:
            # 去除末尾多余的0
            for tmp in range(n):
                nums1.pop()
            for i in range(n):
                nums1.append(nums2[i])
        else:
            for tmp in range(n):
                nums1.pop()
            i = j = 0
            while i != m and j != n:
                if nums1[i] >= nums2[j]:
                    nums1.insert(i, nums2[j])
                    i += 1
                    j += 1
                    # 因为插入了新元素，nums1长度要增加一，即m=m+1
                    m += 1 
                else:
                    i += 1
            if i == m:
                for k in range(j, n):
                    nums1.append(nums2[k])
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 关于注释（A Comment on Comments） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_16/)
我相信大家都明白注释的重要的性，在此我就不赘述为什么要写注释了。虽然现如今有 Javadoc 类似的工具可以解析特定格式的注释以生成文档。但这些远远不够，在某些难以理解的地方，让需要额外的注释来进行更好的解释。

- 注释代码无法表述的内容（Comment Only What the Code Cannot Say） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_17/)
注释和代码一样，都存在这好坏。注释的好坏与注释的多少无太多关系。有些阅读代码很容易理解便不需要注释，比如 if (a>b) // 当a大于b时。注释应该更多的侧重于简单地介绍代码功能，为什么代码要这样做，而不是具体的代码工作方式。

- 持续学习（Continuous Learning） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_18/)
持续学习是相当重要的，在如今的互联网上，提供了多种方式可用于学习，比如：阅读书籍/杂志/博客/文档，在互联网上阅读或解决他人提出的问题或者提出自己问题等待他人解答，加入当地组织，阅读他人的建议并思考和选择适合自己的遵循。

- 便利不是灵活性（Convenience Is not an -ility） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_19/)
API的设计要注重灵活性以应对可能会出现的需求变化等，而不是注重便利性，除非你的软件一旦完成将不再修改。API设计尤其要避开那些特殊性很强的功能，因为他们可能某时便不再需要了。

- 尽早部署（Deploy Early and Often） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_20/)
一般地，给客户部署和安装在项目结束之后。但这并不是一个好方法，因为有可能你会发现客户在使用后提出了新的要求或者是大幅度的需求变更。为了回避这一问题，可以在实现了一个简单的原型后，便可以给客户部署，虽然它无法用于实际生产环境，但客户可以体验它，尝试学习使用它，以及明白项目的进度，同时有问题/新的需求也会提出，这样未后面的开发留下可以回旋的余地。

### Tips
Python中字符串方法str.lower()，str.upper()，str.title()，str.capitalize()的功能如下：
- str.lower()：返回将字符串中所有的大写字符为小写的结果
- str.upper()：返回将字符串中所有的小写字符为大写的结果
- str.title()：返回将字符串“标题化”的结果（标题化指的是所有单词首字母大写，其余字母小写）
- str.capitalize()：返回将字符串首字符大写，其余字母小写的结果
示例代码如下：
```python
s0 = 'an apple A DAY keeps the doctor away.'
s1 = s0.lower()
s2 = s0.upper()
s3 = s0.title()
s4 = s0.capitalize()
print('s0 = ',s0)
print('s1 = ',s1)
print('s2 = ',s2)
print('s3 = ',s3)
print('s4 = ',s4)

'''
输出结果如下：
s0 =  an apple A DAY keeps the doctor away.
s1 =  an apple a day keeps the doctor away.
s2 =  AN APPLE A DAY KEEPS THE DOCTOR AWAY.
s3 =  An Apple A Day Keeps The Doctor Away.
s4 =  An apple a day keeps the doctor away.
'''
```

### Sharing
在 Review 部分中，尽早部署（Deploy Early and Often）的意义和做一个 demo 一样；便利和灵活性比较难以把握，盲目的追求开发时的便利性，很难适应变化性。但是，一味地追求灵活性会大大增加开发的难度；注释的内容要聚焦于**WHAT** your code does，而不是**HOW**，如有必要可以解释下**WHY**。