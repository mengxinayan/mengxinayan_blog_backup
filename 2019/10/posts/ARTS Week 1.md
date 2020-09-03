标题： ARTS Week 1
分类： ARTS
tags： ARTS
-----------------------------------

Oct 28,2019 ~ Nov 3,2019
### Algorithm 
本周的学习的算法是二分法。二分法可以用作查找即二分查找，也可以用作求解一个非负数的平方根等。下面主要以二分查找为例。
为了后续描述方便理解，先作出如下定义：
- k：要查找的数字
- L：待查找的有序序列
- left：查找区间的左边界
- right：查找区间的有边界
- mid：查找区间的中间位置，`mid = (left + right) // 2`

二分查找重要前提：序列L必须**有序**！
二分查找的基本思路如下：
1. 根据 left，right 求 mid。
2. 判断 mid 是否等于 k
3. 若等于，则返回mid，结束。
4. 若不等于，则需要判断 k 与 mid 的大小关系，若 k 小于 mid ，更新 high。反之更新 low
5. 循环1～4步，只要 left <= right

二分法虽然较为简单，但在实现中仍有一些小的细节需要注意：
更新high和low值时需要注意：若在前半部分，更新时应为`right = mid - 1`，若在后半部分，更新时应为`left = mid + 1`。因为mid已经经过判断，所以在更新时要跳过mid。
下面是Python 3语言实现的基本二分查找：
```python
#coding=utf-8

def binary_search(L, k):
    left = 0
    right = len(L) - 1
    while left <= right:
        mid = (left + right) // 2
        if k < L[mid]:
            right = mid - 1
        elif k > L[mid]:
            left = mid + 1
        else:
            return mid
    return -1 # 没有找到

L = [3, 4, 6, 7, 9, 12, 24]
print(binary_search(L, 4))
print(binary_search(L, 8))
```

二分法亦可以用做求解平方根，左右端变为了0和待求解平方跟的数字c，判断条件变为了 $ mid ^ 2 == c $ ，更新mid时不需要减去1，判断结束循环的条件为是否满足精度，即$ abs(mid^2 - c) > 0.0001  $具体实现的代码如下：
```python
#coding=utf-8

def my_square(c):
    left = 0
    right = c
    mid = (left + right) / 2
    while abs(mid * mid - c) > 0.00000001:
        if mid * mid < c:
            left = mid
        else:
            right = mid
        mid = (left + right) / 2
    return mid

print(my_square(10))
```

### Review
本周读的英文技术文章是：[Linux kernel coding style](https://www.kernel.org/doc/html/v4.10/process/coding-style.html)（注：因为文章比较长，而鄙人的英文比较弱，所以本周只有前半部分）
为什么选择这一篇。众所周知，良好的代码风格是易于阅读和理解的。而光靠自己的摸索未必会拥有良好的风格，尤其对那些自认为自己风格还不错的人。（PS：鄙人曾见过认为对代码不进行缩进，而进行的左对齐的人）。阅读他人的风格标准有助于认识到的自己风格中的不足和缺陷。最后，鄙人的观点是风格要统一即可，不一定要完全按照某一具体风格。
下面便是阅读时的具体摘录：
1. 缩进
缩进应为8个空格，理由是因为更容易更看清楚层次关系，再加上一行代码不超过80个字符，这样就可以避免写出层次很深的代码（一般层次深的原因都是因为循环的问题）。而对于switch语句，可能一个case中处理会比较复杂，因此case语句不进行缩进。示例代码如下：
```c
switch (suffix) {
case 'G':
case 'g':
        mem <<= 30;
        break;
case 'M':
case 'm':
        mem <<= 20;
        break;
case 'K':
case 'k':
        mem <<= 10;
        /* fall through */
default:
        break;
}
```
此外，一行代码只写一条语句，不允许出现多条语句
```c
if (condition) do_this;
```

2. 一行代码的列数，不得超过80个字符。若超出，则需要打断，新起一行并分布在右端。

3. 花括号和空格
一、花括号：
- 左花括号大多数情况不换行，且前面用空格分隔。函数定义中的左花括号需要换行
```c
if (x is true) {
        we do y
}

switch (action) {
case KOBJ_ADD:
        return "add";
case KOBJ_REMOVE:
        return "remove";
case KOBJ_CHANGE:
        return "change";
default:
        return NULL;
}
```
```c
int function(int x)
{
        body of function
}
```
- 右花括号大部分情况需要新起一行且后面不跟其他语句。do-while和else-if语句中需要紧跟右花括号
```c
do {
        body of do-loop
} while (condition);

if (x == y) {
        
} else if (x > y) {
        ...
} else {
        ....
}
```
- 什么时候加花括号？总结起来就是，当超过一条语句时则都需要加花括号。if-else语句要加括号则都加，要不加都不加，不能有一个加而另一个不加的情况。
```c
if (condition)
        action();

if (condition)
        do_this();
else
        do_that();

if (condition) {
        do_this();
        do_that();
} else {
        otherwise();
}
```
二、空格
- 大部分关键词后面读需要空格，除了sizeof
`if, switch, case, for, do, while`
- 涉及到指针时，表示指针和去地址时，运算符应该靠近变量名而不是类型名
```c
char *linux_banner;
unsigned long long memparse(char *ptr, char **retptr);
char *match_strdup(substring_t *s);
```
- 二元运算符的左右都需要空格分开
`=  +  -  <  >  *  /  %  |  &  ^  <=  >=  ==  !=  ?  :`
- 一元运算符和前缀/后缀++，--不要用空格分离
`&  *  +  -  ~  !  sizeof  typeof  alignof  __attribute__  defined ++ --`

4. 命名：拒绝大小写混写

5. Typedef的使用
- 尽量避免使用Typedef，对于通过指针或结构体直接访问的则不需要typedef
- 以下情况可以使用Typedef：隐藏某些类型、消除可能因为系统的不同而带来同一类型不同的影响（比如：int）、用于类型检查检查的新类型、于C99标准有冲突

6. 函数
- 函数要尽可能短小，因为标准显示屏是80*24的。函数中的局部变量不应太多，不宜超过5-10个。
- 函数声明时需要包含参数名，不可是仅仅有类型

7. goto的使用
- 尽量避免使用goto语句
- 使用goto的原因为：不需要注释更容易理解、减少嵌套、避免发生错误时产生未定义的行为、减少编译器的工作

8. 注释
- 注释的内容要聚焦于**WHAT** your code does，而不是**HOW**，如有必要可以解释下**WHY**
- 函数的说明注释应放置到函数的外面，而不是函数的内部
- 多行注释的格式：
```c
/*
 * This is the preferred style for multi-line
 * comments in the Linux kernel source code.
 * Please use it consistently.
 *
 * Description:  A column of asterisks on the left side,
 * with beginning and ending almost-blank lines.
 */
```
9. emacs的配置
因为emacs是GNU开发的，对C代码的风格会进行自动修改风格，为了让其满足Kernel的风格，将以下内容增加到`.emacs`文件中。
```lisp
(defun c-lineup-arglist-tabs-only (ignored)
  "Line up argument lists by tabs, not spaces"
  (let* ((anchor (c-langelem-pos c-syntactic-element))
         (column (c-langelem-2nd-pos c-syntactic-element))
         (offset (- (1+ column) anchor))
         (steps (floor offset c-basic-offset)))
    (* (max steps 1)
       c-basic-offset)))

(add-hook 'c-mode-common-hook
          (lambda ()
            ;; Add kernel style
            (c-add-style
             "linux-tabs-only"
             '("linux" (c-offsets-alist
                        (arglist-cont-nonempty
                         c-lineup-gcc-asm-reg
                         c-lineup-arglist-tabs-only))))))

(add-hook 'c-mode-hook
          (lambda ()
            (let ((filename (buffer-file-name)))
              ;; Enable kernel mode for the appropriate files
              (when (and filename
                         (string-match (expand-file-name "~/src/linux-trees")
                                       filename))
                (setq indent-tabs-mode t)
                (setq show-trailing-whitespace t)
                (c-set-style "linux-tabs-only")))))
```

### Tip
Python语言中`A += B`和`A = A + B`的区别：
- 对于不可变的类型，`A += B`和`A = A + B`是没有区别的。
- 对于可变类型， `A += B`是在原值上进行修改的，而`A = A + B`则是新建一个存储计算结果
那么，Python中的可变类型和不可变类型分别有什么：
- 可变类型：Set（集合）、List（列表）、Dictionary（字典）
- 不可变类型：Number（数字）、String（字符串）、Tuple（元组）
测试代码和运行结果如下：
```python
#coding=utf-8

L1 = [1]
L2 = [1]
print('Init id(L1) = '+str(id(L1)))
L1 += [2]
print('Now id(L1) = '+str(id(L1)))
print('Init id(L2) = '+str(id(L2)))
L2 = L2 + [2]
print('Now id(L2) = '+str(id(L2)))
```
运行结果如下：
```
Init id(L1) = 140542507966344
Now id(L1) = 140542507966344
Init id(L2) = 140542507966408
Now id(L2) = 140542506992520
```

### Sharing

ARTS是陈皓大佬的发起的一个活动，具体活动内容不再此处赘述。之前一直想写文章，但又不知道具体该写什么内容，虽然有一些内容想写，但是又怕自己挖坑+写不好。因此借助ARTS活动来提升自己的算法能力、英文阅读能力、文字表达能力以及一些知识点的总结和我个人的思考、感想。以后我会在保证每周ARTS的同时，尽可能写作其他技术内容。

文章若有纰露和不足之处，还望大家批评指正。