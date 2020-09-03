## Spacemacs简单介绍及安装
[Spacemacs官网](https://www.spacemacs.org)
### 为什么选择Spacemacs
Spacemacs是一个已经配好的Emacs和Vim，正如官网所说的`The best editor is neither Emacs nor Vim, it's Emacs and Vim!`
### 具体安装以及安装小建议
1. 预先准备:需要先安装好`Emacs`和`git`
2. 备份原先的配置
```shell
mv .emacs.d .emacs.d.bak
mv .emacs .emacs.bak
```
3. 克隆仓库
```shell
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
```
github可能会连接比较慢，可以使用在国内的码云备份（每天同步一次)
```shell
git clone https://gitee.com/mirrors/spacemacs.git ~/.emacs.d
```
4. (可选)切换分支
默认的分支是`master`分支，经我本人的测试安装，Emacs版本是26.3时，使用`develop`分支更好，切换分支的命令如下：
```shell
git checkout develop
```
5. 初始化设置
```shell
emacs --insecure
```
将会进入emacs后要求选择编辑方式（vim或emacs）、标准版还是精简版
6. 安装所需要的包
如果你的网络情况比较好，那么只需要等待安装完成就好
如果网络情况不太好，可以考虑且换为国内源。具体切换方法如下：
- 先推出emacs，先按`Ctrl-g`再按`Ctrl-x Ctrl-c`。
- 修改`.spacemacs`文件，找到`defun dotspacemacs/user-init ()`函数，在函数中根据[清华大学的镜像](https://mirrors.tuna.tsinghua.edu.cn/help/elpa/)的帮助进行添加，要注意`master`和`develop`分支是不同的，添加后结果如下：
```lisp
(defun dotspacemacs/user-init ()
 "Initialization for user code:
This function is called immediately after `dotspacemacs/init', before layer
configuration.
It is mostly for variables that should be set before packages are loaded.
If you are unsure, try setting them in `dotspacemacs/user-config' first."
    (setq configuration-layer-elpa-archives
       '(("melpa-cn" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")
        ("org-cn"   . "http://mirrors.tuna.tsinghua.edu.cn/elpa/org/")
        ("gnu-cn"   . "http://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")))
  )
```
- 修改镜像后，重新启动emacs，等待安装结束即可
### 安装结果
(Spacemacs首页截图)