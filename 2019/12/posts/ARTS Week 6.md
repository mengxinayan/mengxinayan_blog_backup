标题： ARTS Week 6
分类： ARTS
tags： ARTS
-----------------------------------

Dec 2, 2019 ~ Dec 8, 2019
### Algorithm
从本周开始，由于要涉及某一算法，但我又有选择困难症。所以我决定在Leetcode刷题的，用ARTS中的算法部分来记录本周值得记录的一道题，也可以理解成某一题目的详解吧。本周的题目如下：

Problem 14. Longest Common Prefix - 最长公共前缀 [题目链接](https://leetcode-cn.com/problems/longest-common-prefix/)

题目描述：给定某一个字符串数组，找到该字符串数组中所有字符串的最长公共子串。如果没有，则返回空字符串。下面是两个例子：
例一：
Input: ["flower","flow","flight"]
Output: "fl"
例二：
Input: ["dog","racecar","car"]
Output: ""

思路：先对特殊情况（没有字符串或者只有一个字符串）进行处理。而后计算出所有字符串中最短字符串的长度，因为公共字符串长度不会超过它。而后从第一个字符串开始遍历，检查某个字符是否在所有字符串中是否出现且出现的位置相同，若是，将该字符加入字符串；若不是，则停止循环。

通过的代码如下
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0:
            return ''
        if len(strs) == 1:
            return strs[0]
        lens = []
        for i in range(len(strs)):
            lens.append(len(strs[i]))
        minlen = min(lens)
        res = ''
        for i in range(minlen):
            ch = strs[0][i]
            flag = True
            for j in range(1, len(strs)):
                if ch != strs[j][i]:
                    flag = False
            if flag == True:
                res += ch
            else:
                break
        return res
```

### Review
Linux Powertop 的介绍和使用。[原文链接](https://www.2daygeek.com/powertop-monitors-laptop-battery-usage-linux/)。注：下面的内容结合了一些其他文章/资料汇总写成的，在需要时我也会给出链接。
装了 Linux 系统的笔记本电脑或其他类似设备，其电源管理也许并没有Windows下高效。Powertop 便是一个由 Intel 发布的工具，可以用来诊断电池使用情况，哪些设备、进程最消耗电池，以及可以给出相应的优化建议。并且它是开源的，开源协议为GPL-v2.0，[Github仓库地址](https://github.com/fenrus75/powertop)。更多介绍见[官网](https://01.org/powertop)和[维基百科](https://en.wikipedia.org/wiki/PowerTOP)
在很多发行版的仓库中，都含有 Powertop。安装方法具体如下：
```bash
# For Ubuntu/Debian
% sudo apt install powertop
# For RHEL/CentOS
% sudo yum install powertop
# For Fedora
% sudo dnf install powertop
# For Arch/Manjaro
% sudo pacman -S powertop
# For SUSE/openSUSE
% sudo zypper install powertop
```
powertop的使用也比较简单，具体使用方法如下：
```bash
% sudo powertop
PowerTOP v2.9     Overview   Idle stats   Frequency stats   Device stats   Tunables                                     
The battery reports a discharge rate of 12.6 W
The power consumed was 259 J
The estimated remaining time is 1 hours, 52 minutes

Summary: 1692.9 wakeups/second,  0.0 GPU ops/seconds, 0.0 VFS ops/sec and 54.9% CPU use

                Usage       Events/s    Category       Description
              9.3 ms/s     529.4        Timer          tick_sched_timer
            378.5 ms/s     139.8        Process        [PID 2991] /usr/lib/firefox/firefox -contentproc -childID 7 -isForBrowser -prefsLen 8314 -prefMapSize 173895 -schedulerPrefs 00
              7.5 ms/s     141.7        Timer          hrtimer_wakeup
```
最上面的一列，Overview，Idle stats，Frequency stats，Device stats，Tunables 便是各种页面，可以使用 Tab 键在各个页面之间切换。使用 Esc 键可以退出界面。
但是，终端的界面看起来不是很方便（个人感觉），powertop 也提供了将报告生成为 HTML 文件方便进行查看
```bash
# 以下几种方式效果都相同
% sudo powertop -r # 在当前目录下生成 HTML 报告，文件名为 powertop.html
% sudo powertop --html # 同上
% sudo powertop --html report.html # 在当前目录下生成 HTML 报告，文件名为 report.html
```
通过浏览报告，便可以得知哪些进程/设备对电源的消耗较多，且存在可以优化的地方，这样便可以进行相应调整。但是，我相信很多人和我一样，不愿意去阅读详细的报告，只想轻松地达到目的。为了照顾我这样的懒人，powertop 也提供了让其自动调优选项，使用方法如下：
```bash
% sudo powertop --auto-tune
```

### Tips
Python中类内使用递归函数的方法如下：
```python
class Example:
    def func(self, x):
        return self.func(x-1) + 1
```

### Sharing
《左传-庄公·庄公十年》中有句“一鼓作气，再而衰，三而竭”。个人对此有一些感触，前面5周的ARTS还按照时间写下来了，但由于第六七周忙于某些事情，没有来得及写（当然，最主要的问题还是出在自己的时间管理上）。结果导致整整一个多月的 ARTS 延误了，现在我准备重新把荒废的 ARTS 拾起来，先把当初欠下的好几篇补上来。为了能节约发布的时间，所以暂时不打算写好一篇就发一篇，而是把 ARTS 的进度追上当前的周数时，再统一发出。