标题： ARTS Week 3
分类： ARTS
tags： ARTS
-----------------------------------

Nov 4,2019 ~ Nov 10,2019
### Algorithm
本周主要的算法是如何求两个数的最大公因数。传统的想法便是对这两个数分解质因数，而后找到其公共因数，再相乘，这样就会得到最大公因数了。话不多说，直接看代码吧。
```python
# 求解一个数字x的质因数。注意循环的范围，若在范围内没有找到因数，则说明它是一个素数
import math
def factors(x):
    y = int(math.sqrt(x))
    R = []
    for i in range(2, y+1):
        if x % i == 0:
            R.append(i)
            R = R + factors(x//i)
            break
    else:
            R = [x]
    return R

def product(L):
    y = 1
    for i in L:
        y = y * i
    return y

def GCD_factors(x, y):
    Lx = factors(x)
    Ly = factors(y)
    def search_and_delete(a, L):
        for i in range(len(L)):
            if L[i] == a:
                return True, L[:i] + L[i+1:]
        return False, L
    R = []
    for e in Lx:
        found, Ly = search_and_delete(e, Ly)
        if found:
            R.append(e)
    return product(R)
```
但是，显然可以看出，先求解因数，再求解公共因数集合，最后相乘得到结果。这种算法求解最大公因数的时间开销是较大的，虽然便于理解。那还有一种更快的求解方法，那就是辗转相除法（又称欧几里德算法），算法主要用到了一个等式，具体如下：
- GCD：求解x，y的最大公因数
- mod：求余数。例如$a \bmod b$表示求解a除以b的余数
- 注，下面的描述中假设$ a > b $

$$ GCD(a,b) = GCD(b, a \bmod b) $$

下面用实际计算过程作为一个例子：
$ GCD(12, 8) = GCD(8, 12 \bmod 8) = GCD(8, 4) = GCD(4, 8 \bmod 4) = GCD(4, 0) = 4 $

有了上面的描述，那么代码就很好写了，代码如下：
```python
def GCD_Euclid(x, y):
    if x < y:
        x, y = y, x
    if x % y == 0:
        return y
    return GCD_Euclid(y, x % y)
```

### Review
本周继续上周的没有完成的文章，[Linux Kernel coding style](https://www.kernel.org/doc/html/v4.10/process/coding-style.html)，开始吧

10. Kconfig文件
Kcinfig文件的缩进有所不同，而其中的help只需要两格缩进，如果有危险的地方，需要用大写提醒。缩进格式如下。
```
config AUDIT
      bool "Auditing support"
      depends on NET
      help
        Enable auditing infrastructure that can be used with another
        kernel subsystem, such as SELinux (which requires this for
        logging of avc messages output).  Does not do system-call
        auditing without CONFIG_AUDITSYSCALL.
config ADFS_FS_RW
      bool "ADFS write support (DANGEROUS)"
      depends on ADFS_FS
```
11. 数据结构：数据结构需要注意的要进行**引用计数**，以防止产生垃圾和遭遇锁定。

12. 宏定义，枚举
宏定义和枚举类型的变量必须使用大写。
```c
#define CONSTANT 0x12345
```
宏定义的函数可以像普通函数一样，函数名采用小写。但要尽量避免写宏定义函数，可以用内联函数去替代。使用宏定义函数有如下几个需要注意的地方，下面的例子均为反例
- 不要影响控制流
```c
#define FOO(x)                                  \
        do {                                    \
                if (blah(x) < 0)                \
                        return -EBUGGERED;      \
        } while (0)
```
- 避免依赖于局部变量
```c
#define FOO(val) bar(index, val)
```
- 不要用作左值
```c
FOO(x) = y;
```
- 注意优先级，宏定义函数中宏定义变量要用括号扩起来
```c
#define CONSTANT 0x4000
#define CONSTEXP (CONSTANT | 3)
```
- 在其中定义局部变量时，注意和已有的变量名冲突
```c
#define FOO(x)                          \
({                                      \
        typeof(x) ret;                  \
        ret = calc_ret(x);              \
        (ret);                          \
})
```

13. 打印内核消息，尽量使用简短正式的语言，准确的描述信息。

14. 分配内存
为结构体分配内存尽量使用如下代码：
```c
p = kmalloc(sizeof(*p), ...);
```
分配数组尽量使用如下代码：
```c
p = kmalloc_array(n, sizeof(...), ...);
```
分配归零数组尽量使用如下代码：
```c
p = kcalloc(n, sizeof(...), ...);
```

15. 内联函数。
大量的使用`inline`会导致CPU中的icache占用量更大，从而带来无法命中，反而降低了效率。
内联要尽可能简单，文章中给出的建议代码行数不要多于三行。例外情况是，参数是编译时常量。

16. 函数返回值和类型
bool类型和整数类型的滥用可能会带来风险，虽然有时编译器能帮我们发现这些。
当函数表示动作或命令时，返回值类型应为整数
当函数表示谓词（比如是否）时，返回值类型应为bool

17. 不要重新发明内核宏
如果内核中已有某功能的宏函数，那么不要自己编写函数。比如计算数组的长度。请利用如下宏函数。
```c
#define ARRAY_SIZE(x) (sizeof(x) / sizeof((x)[0]))
```

18. 不要把个人的对编辑器的设置存放到代码中

19. 内联汇编
大量的汇编代码要放到`.s`文件中。
也许会需要把汇编代码标记为`volatile`，以防止GCC在将它去除
若有多行汇编，每行汇编要新起一行，不要放在一行代码里。
```c
asm ("magic %reg1, #42\n\t"
     "more_magic %reg2, %reg3"
     : /* outputs */ : /* inputs */ : /* clobbers */);
```
20. 条件编译
不要将条件编译语句放到`.c`文件中
条件编译最小范围应为函数，而不是表达式等其他

### Tip
在Python中，列表的分片会带来复制产生新列表。而使用索引就不会带来这个问题。在一些函数中，参数使用索引来控制访问列表可以提高效率，尤其是在一些递归函数中，因为自始自终列表都没有发生变化。

### Share
看完Linux内核代码风格，虽然有一些东西我在编写C语言时基本没有使用过（有可能是我没有涉及到），但仍有一些东西还是让我有了一些新的知识。就比如内联函数，我之前的了解是那只是对编译器的一种建议，并不一定会内联。从来不知道内联函数过多会带来性能较低的问题。当然文章里面也有一些东西我认为是很正常的要求，比如内联汇编有多行需要换行，但文中仍提及到了，那说明还是有些人并不如此认为