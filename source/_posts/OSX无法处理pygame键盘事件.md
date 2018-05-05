---
title: OSX无法处理pygame键盘事件
tags: Mac
categories:
  - 填坑指南
abbrlink: 967984865
date: 2018-02-09 13:39:27
toc: true
---

 在使用 mac 学习 GTK+时就发现打开的窗口系统不太灵敏，然而由于没有深入学习，所以并没有理会，然而出来混总是要还的，学习 Python 做有关 pygame 的实践时，不管怎么按键盘，窗口上的小飞机死活不动，根本无法检测键盘响应事件。网上换了几种关键词，查了几个英文网站终于找到一个可行的方法，谷歌老爹翻译大法好。下面贴出步骤。

<!--more-->

### 步骤：

#### 第一步

*   确认是否安装 xquartz 最新版本，不是的话点击安装[xquartz](http://xquartz.macosforge.org)。

#### 第二步

*   打开终端控制台，逐行运行下列代码:

```bash
$ ruby -e $ ( curl -fsSLhttps://raw.githubusercontent.com/Homebrew/install/master/install)
$ sudo brew doctor  
$ brew update  
$ brew install python3  
$ brew install sdl sdl_image sdl_mixer sdl_ttf portmidi mercurial  
$ brew install libogg libvorbis  
$ brew install sdl_mixer --with-libvorbis
```

*   如果出现反馈说'xxx already install'，将'install'换成'reinstall'重新运行

#### 第三步

*   安装 Pygame，在终端运行如下代码，其中把'yourname'改为你的用户名，忘记的朋友可以先运行‘ls /Users’查看。

```bash
$ cd /Users/YourName/Downloads  
$ hg clone https://bitbucket.org/pygame/pygame  
$ cd pygame  
$ cd src  
$ pip3 install /Users/YourName/Downloads/pygame  
```

*   到这里 Pygame 所需要的环境就整理好了

#### 第四步

*   在终端运行程序的朋友，三步完就可以试试效果了。如果是用的 IDE 必须把 IDE 的 Python 解释器路径换成我们刚刚更新的那个，这里仅介绍 Pycharm 更改方式，其他的类似。
*   在终端输入

```bash
$ which python3
```

*   记住所得路径。
*   在 Pycharm 按路径:Pycharm->Preferences->Project->Project Interpreter 找到 Project Interpreter 选项框。
*   点击选项框旁边的齿轮按钮选择‘Add Local’按钮 。
*   点击‘system Interpreter’,在选项框选择刚刚记住路径的 Python3(一般系统会自带一个，一定要分清)，或者在旁边的路径里面输入刚刚的路径。
*   完成，等待环境更新完毕即可。
    > 看着动起来的飞船不免还是有些小小的激动.  
    > 网上还有一种方案看上去简洁的多，不过我没有成功，在此贴出来:
    >
    > 1.  remove python3 by pyenv  
    >     `$:pyenv uninstall python3`
    > 2.  remove pyenv  
    >     `$:brew uninstall pyenv`
    > 3.  reinstall python3 by homebrew  
    >     `$:brew install python3`

参考：  
[在 mac 系统上 pygame 不能获得键盘事件](http://bbs.fishc.com/thread-95321-1-1.html)  
[Program Arcade Games With Python And Pygame](http://programarcadegames.com/index.php?chapter=foreword&lang=cn#section_0)
