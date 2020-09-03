标题： ARTS Week 4
分类： ARTS
tags： ARTS
-----------------------------------

Nov 18, 2019 ~ Nov 24, 2019
### Algorithm
深入优先搜索-马遍历棋盘
要求：给定一个`n * m`的棋盘，左上角为(0, 0)，马的初始位置为(x, y)，找到所有方案使得马不重复地遍历棋盘，输出所有方案
#### 思路
马走‘日’字，因此有八种移动方案，分别为：
```python
dir = [[-2,1], [-1,2], [1,2], [2,1], [2,-1], [1,-2], [-1,-2], [-2,-1]]
```
坐标`(x, y)`移动一步后的结果为`(x+dir[i][0], y+dir[i][1])`
马的移动需要受到以下两个条件的约束:
1. 移动后的点仍要在棋盘上，即
$ 0 \leq x+dir[i][0] \leq n-1 $
$ 0 \leq y+dir[i][1] \leq m-1 $
2. 移动后的点是要为访问过的，即
$ visited[x+dir[i][0]][y+dir[i][1]] $
#### 实现
Python的实现代码如下：
```python
def draw():
    print('第', ans,'种方案：',history)

def horse(x, y, step):
    if step == num:
        global ans, found
        ans = ans + 1
        found = True
        draw()
    else:
        for i in range(8):
            x_temp = x + dir[i][0]
            y_temp = y + dir[i][1]
            if 0 <= x_temp < n and 0 <= y_temp < m and visited[x_temp][y_temp] == 0:
                history[step] = [x_temp, y_temp]
                visited[x_temp][y_temp] = 1
                horse(x_temp, y_temp, step+1)
                visited[x_temp][y_temp] = 0
```
### Review
[Emacs is Sexy](https://emacs.sexy/)
文章介绍的Emacs好处和安装Emacs
1. Why
- 多种主题，[具体介绍](https://emacsthemes.com/)
- 支持多种语言
- 对于vim用户，可以采用[spacemacs](https://www.spacemacs.org)或这安装[Evil Mode](https://github.com/emacs-evil/evil)这个插件
1. 安装
- GNU/Linux：包管理器中就包含有Emacs
- Mac OS X：可以通过Homebrew或者[Emacs For Mac OS X](https://emacsformacosx.com/)
- Windows：[GNU官方](http://gnu.c3sl.ufpr.br/ftp/emacs/windows/)
3. 学习
阅读自带的教程`Ctrl+h t`或者查看[手绘图](https://sachachua.com/blog/2013/05/how-to-learn-emacs-a-hand-drawn-one-pager-for-beginners/)
中文教程可以查看**子龙山人**的教程，[链接](http://book.emacs-china.org/)

希望能开箱即用的用户，可以采用[Spacemacs](https://www.spacemacs.org/)。至于 Spacemacs 如何安装，可以看我的这篇文章：[Spacemacs 简单介绍及安装]()

### Tips
python3 输入一行数字中间用空格相隔的读取方法，例如：s = '1 2 3 4 5'，如何提取为数组 nums = [1,2,3,4,5]
```python
#方法1
num = [int(n) for n in input().split()]

#方法二
num = list(map(int, input().strip().split()))

print(num)
```
### Share
[Spacemacs 简单介绍及安装]()