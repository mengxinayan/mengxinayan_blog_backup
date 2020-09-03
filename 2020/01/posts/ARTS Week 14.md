标题： ARTS Week 14
分类： ARTS
tags： ARTS
-----------------------------------

Jan 27, 2020 ~ Feb 2, 2020
### Algorithm
Problem 160.Intersection of Two Linked Lists（相交链表）    [题目链接](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

题目描述：给定两个链表，判断其是否存在相交，若存在则返回相交节点，若不存在则返回 null。假设链表中不存在环路，函数不能破坏链表原有结构。举例，下面的两个链表则为相交链表，相交结点为 9。
1 -> 2 -> 3
           \
            9 -> 8
           /
          7

思路1：与上一周的题目类似，可以将其中一个链表中所有结点的地址用一个集合进行保存，接下来便利另一个链表，若其中出现某个结点地址也出现在了集合中，那么说明两个链表相交，若遍历结束也没有出现，则说明两个链表不相交
通过的代码如下
```python
# Solution 1

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        if (headA == None) or (headB == None):
            return None
        node_id_A = set([])
        p = headA
        while p != None:
            node_id_A.add(id(p))
            p = p.next
        q = headB
        while q != None:
            if id(q) in node_id_A:
                return ListNode(q.val)
            q = q.next
        return None
```

思路2：使用两个指针进行判断。先进行遍历，若两个链表的末尾元素不相同，则说明两个链表必定不相交（注：若相交则末尾元素相同，但是末尾元素相同**未必相交**！）。假设两个链表相交，那么该如何找到相交元素呢？设两个链表分别为A , B，相交部分为 C，两个指针 p，q 分别先指向 A，B，当遍历链表到末尾时，让 p 指向B，q 指向 A，继续遍历，当 p，q相等时，则说明该节点为开始相交的节点，原因很简单，因为在找到相交的节点时，p 遍历了 len(A) + (len(B) - len(C)) 个元素，q遍历了 len(B) + (len(A) - len(C)) 个元素，二者是相等的。故因此可以找到相交节点。
通过的代码如下
```python
# Solution 2

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        if (headA == None) or (headB == None):
            return None
        p = headA
        q = headB
        while p.next != None:
            p = p.next
        while q.next != None:
            q = q.next
        if p.val != q.val:
            return None
        else:
            p = headA
            q = headB
            while p != q:
                if p.next == None and q.next != None:
                    p = headB
                    q = q.next
                elif q.next == None and p.next != None:
                    q = headA
                    p = p.next
                else:
                    p = p.next
                    q = q.next
            if p == None:
                return None
            else:
                return ListNode(p.val)
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 大师神话（The Guru Myth） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_36/)
在软件行业有许多闻名的大师，但事实上，“大师”也是人类，他们思考问题时的逻辑方法很我们没什么太多区别。只不过因为经验等积累的较多，“大师”可以利用思维捷径和直觉来发现和解决问题。当然，天赋资质方面仍存在差异，但对大多数人来说，这一点并不明显。

- 努力工作没有回报（Hard Work Does not Pay Off） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_37/)
由于编程和软件开发涉及一个连续的学习过程，你始终需要去学习新的知识。比如阅读书籍，参加会议，与其他专业人员交流，尝试新的技术，简化现有工具等。如果你在项目上花费的时间太多了，既无法保证项目的质量，也无法提升自己。

- 使用 bug 追踪器（How to Use a Bug Tracker） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_38/)
一个好的 bug 报告需要三件事：1）如何尽可能的重现该错误，以及指出该错误发生的频率；2）正常运行应该发生/进行什么操作；3）实际上发生了什么。bug 追踪器除了 bug 报告以外，仍需要记录发现者，bug紧急程度，修复 bug 的人，是否完成修复等。

- 通过删除代码来改进代码（Improve Code by Removing It） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_39/)
少即是多，任何项目中有许多不必要的代码，我们可以通过删除这些代码已达到改进的目的。不必要的代码一办出现在哪里呢？最常见的地方便是“无用”的功能，项目中有一些功能，虽然设计时觉得很有用，但实际情况是很少有用户使用，因此这些功能涉及到的代码便可以去除。当然，还有很多冗余的代码分布在算法设计，数据结构的设计等

- 安装程序（Install Me） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_40/)
任何软件都应该编写一份安装说明。对于有GUI的软件，安装过程一般不是很复杂。但对于没有GUI的软件，例如某工具、库等，你应该为其写一个文档来告诉使用者如何安装/使用它。

此外，分享一篇我在 Linux 中国翻译的文章：[查看 Linux 系统中进程和用户的内存使用情况](https://linux.cn/article-11849-1.html)

### Tips
JavaScript 中 NaN 这个特殊的Number与所有其他值都不相等，包括它自己。唯一能判断NaN的方法是通过isNaN()函数：
```js
NaN === NaN; // false
isNaN(NaN); // true
```

### Sharing
我本周试着参与了一下上周提及的 [Linux 中国翻译计划](https://linux.cn/lctt/)，发现参加起来还是比较容易的，可供选择的题目也不少，每天也有新的题目入选，维护者也比较积极，每天都会处理新的PR。普通人的参与方式是作为译者，想将自己准备翻译的英文文章中一些信息进行修改并提交PR，等翻译好更新文章内容，再次提交新的PR，总结一下，就是翻译一篇文章共需要提交两个PR。等翻译的文章经过校对以后，便会公开发布。在 Review 部分中，我分享了我自己翻译的第一篇文章。