标题： ARTS Week 13
分类： ARTS
tags： ARTS
-----------------------------------

Jan 20, 2020 ~ Jan 26, 2020
### Algorithm
Problem 141 Linked List Cycle (环形链表)   [题目链接](https://leetcode-cn.com/problems/linked-list-cycle/)

题目描述：给定一个链表，判断链表中是否存在环形。pos 代表链表末尾指向的连接到链表的位置，从0开始。若 pos = -1 则表示链表中没有环（注意：输入的只有链表本身，没有 pos）
举例：
Input: head = [3,2,0,-4] (pos = 1)
Output: true
3 -> 2 -> 0 -> -4
     \          /
      \ <------/

Input: head = [3,2,0,-4] (pos = -1)
Output: false
3 -> 2 -> 0 -> -4 -> None

思路1：因为每个结点的地址是唯一的，在 Python 中，id 函数可以求得某个对象的内存地址。可以将这些对象的内存地址保存在一个集合中。因此遍历链表，若某个结点的地址未在集合中，将其地址加入到集合中，若已在集合中，说明链表存在环形。如果链表遍历结束到 None 仍未发现重复出现的结点，那么可以说明链表中不存在环形。
通过的代码如下
```python
# Solution 1

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        node_id = set([])
        res = True
        while head != None:
            if id(head) not in node_id:
                node_id.add(id(head))
            else:
                break
            head = head.next
        else:
            res = False
        return res
```

思路2：可以设置两个指针，一个逐个遍历链表称为慢指针，一个每次隔一个遍历链表称为快指针，起始时，快指针比慢指针靠前一个位置，如果链表中存在环形，那么就好比操场上跑圈一样，快的终有一刻会和慢的相遇（快的超过慢的一圈）。如不存在环形，那么快指针将优先到达结束的结点
通过的代码如下
```python
# Solution 2

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if head == None:
            return False
        elif head != None and head.next == None:
            return False
        else:
            slow = head
            fast = head.next
            res = False
            while slow != fast:
                if (fast.next == None) or (fast.next.next == None):
                    break
                slow = slow.next
                fast = fast.next.next
            else:
                res = True
            return res
```

### Review
本周继续 Review 每个程序员需要知道的97件事（英文名：97 Things Every Programmer Should Know）。[原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/)。下面是本周的5个小内容：
- 不要触摸该密码（Don't Touch that Code!） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_31/)
我们应该不同用途的机器设置不同的密码，且不同任务的人应该知道不同的代码。比如开发人员本地机器、开发服务器和生产服务器。其中开发服务器的密码重要程度没有生产服务器高，不应该让所有的人都有权限去访问生产服务器。

- 封装行为，而不是状态（Encapsulate Behavior, not Just State） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_32/)
面向对象的一大特点便是封装，封装的一个重要的要求便是对行为/操作进行封装，而不是操作前后的状态。比如一个门对象，它有四个状态：打开，关闭，正在打开，正在关闭。而这四个状态的转换只需要两个操作便可以完成：开门，关门。

- 浮点数不是实数（Floating-point Numbers Aren't Real） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_33/)
在计算机底层，浮点数的实现和整数的实现是不同的。整数在底层是可以准确表达的，而浮点数都是近似的。因此，在一些高精度计算中，可能会由于浮点数近似的问题带来意想不到的后果。这就是为什么 linux 内核和金融程序/科学计算程序中很少使用浮点数，而是去一些十进制类用于代替。

- 用开源实现你的抱负（Fulfill Your Ambitions with Open Source） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_34/)
也许你渴望能加入微软，亚马逊等大企业，但是有一个更好的办法，那就是利用开源，现如今开源项目众多，可以轻松的找到你感兴趣的方向。如果从零开始发起一个开源项目有难度，那么，一个更好的办法便是加入已有的项目，你可以帮忙参与开发，找出bug，或者编写/完善文档。

- API设计的黄金法则（The Golden Rule of API Design） [原文链接](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_35/)
API设计的黄金法则是：仅仅为开发的API编写测试是不够的，要为使用该API的代码编写进行单元测试。

### Tips
JavaScript 中 '=='和'==='的区别：`==`比较，它会自动转换数据类型再比较，很多时候，会得到非常意想不到的结果；`===`比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较值是否相同。

### Sharing
除了正在翻译的程序员应该知道的97件事之外，我还发现另一个比较好的可以翻译的文章，那边是 Linux 中国翻译计划，里面有很多已经选好的文章等待翻译，你可以找到自己感兴趣的文章进行翻译，一些具体的介绍和如何参与的方式，可以在如下链接中找到答案：[Linux 中国 翻译组](https://linux.cn/lctt/)