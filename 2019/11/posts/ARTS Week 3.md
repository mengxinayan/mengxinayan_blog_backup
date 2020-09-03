标题： ARTS Week 3
分类： ARTS
tags： ARTS
-----------------------------------

Nov 11,2019 ~ Nov 17,2019
### Algorithm
本周来介绍快速求一个数字n次方的余数。
#### 理论基础
我们先定义运算$ x \bmod p = r $与$ x \equiv r \pmod p $的含义是一样的。若$ p = 5 $，则可以将所有整数划分到5个不相交的集合里，具体如下：
$$
\left\{\begin{matrix}
 & \{\dots -10, -5, 0, 5, 10 \dots \} \bmod 5 = 0 & \\ 
 & \{\dots -9, -4, 1, 6, 11 \dots \}  \bmod 5 = 1 & \\
 & \{\dots -8, -3, 2, 7, 12 \dots \}  \bmod 5 = 2 & \\
 & \{\dots -7, -2, 3, 8, 13 \dots \}  \bmod 5 = 3 & \\
 & \{\dots -6, -1, 4, 9, 14 \dots \}  \bmod 5 = 4 & \\
\end{matrix}\right.
$$
可能有人不懂为什么$-4 \bmod 5 = 1$，我来解释一下，因为$ -4 = 5 \times (-1) + 1 $，故$ -4 \div 5 = -0.8 = -1 \cdots 1 $。因此$-4 \bmod 5 = 1$
那么根据上面的描述，就可以将数之间的运算通过取余映射在有限个集合内。那么，有如下两条基本性质，可以更加方便我们进行求解
1. 若存在 $ a \equiv b \pmod p, c \equiv d \pmod p $ ，则 $ a+c \equiv b+d \pmod p $
2. 若存在 $ a \equiv b \pmod p, c \equiv d \pmod p $ ，则 $ a*c \equiv b*d \pmod p $

通过这样的性质就很容易求解一个大数的对某个数字取余的结果。以计算$(2^{32} + 5)\bmod 7 = ?$为例
1. $ 2 \bmod 7 = 2 $
2. $ 2^2 \bmod 7 = (2 \times 2) \bmod 7 = 4$
3. $ 2^4 \bmod 7 = (2^2 \times 2^2) \bmod 7 = 4 \times 4 \bmod 7 = 2 $
4. $ 2^8 \bmod 7 = {2^4 \times 2^4} \bmod 7 = [(2^4 \bmod 7) \times (2^4 \bmod 7)] \bmod 7 = (2 \times 2) \bmod 7 = 4 $
5. $ 2^{16} \bmod 7 = {2^8 \times 2^8} \bmod 7 = [(2^8 \bmod 7) \times (2^8 \bmod 7)] \bmod 7 = (4 \times 4) \bmod 7 = 2 $
6. $ 2^{32} \bmod 7 = (2^{16} \times 2^{16}) \bmod 7 = [(2^{16} \bmod 7) \times (2^{16} \bmod 7)] \bmod 7 = (2 \times 2) \bmod 7 = 4 $
7. $ (2^{32}+5) \bmod 7 = [(2^{32} \bmod 7) + (5 \bmod 7)] \bmod 7 = (4 + 5) \bmod 7 = 2 $
#### 具体实现
设问题为：求解$ a^x \bmod b = ? $。因此问题的关键在于如何分解$x$，具体有两种基本思路，分别是按照`2`和`10`进行分解。当然也可以按照其他数进行分解，但实现起来较复杂。
1. 按数字2来分解，分解的基本原理如下:
$$
\begin{cases}
 & x = x // 2 + x // 2,\quad a^x = a^{x//2} \times a^{x//2} \quad \text{ if } x \bmod 2 = 0 \\ 
 & x = x // 2 + x // 2 + 1,\quad a^x = a^{x//2} \times a^{x//2} \times a \quad \text{ if } x \bmod 2 = 1
\end{cases}
$$
根据上述公式不难写出代码：
```python
def my_mod(a, x, b):
    if x == 1:
        return a % b
    else:
        tmp = my_mod(a, x//2, b)
        if x % 2 == 0:
            return ( tmp * tmp ) % b
        else:
            return ( tmp * tmp * my_mod(a, 1, b) ) % b
```
2. 按数字`10`来分解，分解的基本原理如下，因为是递归的，为了方便理解，使用数字123为例:
$ 123 = (1 \times 10 + 2) \times 10 + 3 $
$ a^{123} = ({3^1}  **  3^{10} \times 3^2 ) ** 3^{10} \times 3^3 $
实现代码如下：
```python
def my_mod(a, x, b):
    def cal_mod(a, b):
        L = []
        for i in range(11):
            L.append( (a**i) % b )
        return L

    def recursive(x):
        if 0 <= x <= 9:
            return L[x]
        else:
            return ( recursive(x//10) ** L[10] * recursive(x%10) ) % b

    if 0 <= x <= 10:
        return (a**x) % b
    L = cal_mod(a, b)
    return recursive(x)
```
### Review
Why is the gets function so dangerous that it should not be used?
在一个比较早的代码时，运行总会出错，后面通过查找资料，发现是`gets`函数的问题。
当我查阅gets函数时发现，在*DESCRIPTION*部分直接写道**Never use this function.**
在阅读了一些关于`gets`英文文章后，我明白了为什么`gets`会带来问题。
简单地说，带来隐患的根源在于`gets`函数不会控制读入的量，而只是以`\n`或`\0`作为读入的终止。例如下面这个代码：
```c
#include<stdio.h>

int main()
{
    char str1[] = "hello";
    char str2[] = "world";
    char *str = gets(str1);
    return 0;
}
```
程序开始运行后，输入任意个字符，点击回车将会直接带来段错误从而终结程序。

### Tips
根据上述的描述，凡要涉及到`gets`函数，都可以使用`fgets`函数进行代替
fgets函数原型如下
```c
char *fgets(char *s, int size, FILE *stream);
```
从标准输入的读取方法如下：
```c
char buffer[100];
while (fgets(buffer, sizeof(buffer), stdin))
{
    // operations
}
```

### Share
本周分享一个关于vim配置的项目——[VimPlus](https://github.com/chxuan/vimplus)
不少vim用户都喜欢安装或多或少的插件以增强原生vim的功能，但不少新手第一次安装插件时可能会遇到某些问题，同时也未必会一次安装配置好需要的插件。而这个项目就是为了方便新手可以通过简单的运行命令就可以安装许多常用的插件，进而配置出一个像IDE似的vim。
其中可以一键安装的插件包括`vim-plug`、`You Complete Me`等
目前项目的作者的维护也比较及时。希望未来可以越做越好！
更多内容可去上述项目链接中进行查看。
（注:我与作者没有任何联系，只是发现了这个项目并且个人尝试后觉得不错，所以分享在这里）