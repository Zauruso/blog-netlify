---
title: HTML基础一
mathjax: false
toc: true
top: false
tags:
  - 前端
  - HTML
categories:
  - 前端学习笔记
abbrlink: 3782454218
date: 2018-05-03 22:15:51
---

<!-- more-->

##  基础概念

### Web 标准

#### w3c 万维网联盟组织

用来制定 web 标准的机构组织

* W3C 指万维网联盟（World Wide Web Consortium）
* W3C 是一个会员组织
* W3C 的工作是对 web 进行标准化
* W3C 创建并维护 WWW 标准
* W3C 标准被称为 W3C 推荐（W3C Recommendations）

### 网页构成

#### HTML+CSS+Js

| 结构 | 表现 |    行为    |
| :--: | :--: | :--------: |
| HTML | CSS  | Javascript |

* Html 制作网页
* Css 对网页进行美化
* Js 让网页动起来

#### HTML 简介

html (Hyper Text Markup Language ) 中文译为“超文本标记语言”，主要是通过 html 标记对网页中的文本，图片，声音等内容进行描述。

### 浏览器

#### 常用的浏览器

IE、火狐（Firefox）、谷歌（Chrome）、Safari 和 Opera

#### 浏览器内核

|   IE    | Firefox | Chrome | Safari | Opera |
| :-----: | :-----: | :----: | :----: | :---: |
| trident |  gecko  | blink  | webkit | blink |

浏览器内核即渲染引擎，决定了浏览器如何显示  网页内容以及页面格式信息。 ===> 浏览器兼容问题

## HTML 标签语法及要点

### 单标签

* 注释标签 `<!-- -->`
* 换行标签 `<br />`
* 水平线标签 `<hr />`

### 标题标签 h1 - h6

|  h1  |  h2  |   h3    |  h4  |   h5    |  h6  |
| :--: | :--: | :-----: | :--: | :-----: | :--: |
| 32px | 24px | 18.72px | 16px | 13.28px | 12px |

**_SEO 优化: h1 在一个页面中只出现一次，为搜索引擎提供关键信息_**


### 文本标签

#### 常用文本标记

* 强调 `<strong></strong>` or`<b></b>`
* 斜体 `<em></em>` or `<i></i>`
* 删除线 `<del></del>` or `<s></s>`
* 下划线 `<ins></ins>` or `<u></u>`

#### 文本标记语义化

<table>
    <tr>
        <td>语义样式标签</td>
        <td> strong - em - del - ins</td>
    </tr>
    <tr>
        <td> strong </td>
    <td>代表内容的强烈的重要性、严重性或者紧急性。</td>
    </tr>
    <tr>
        <td>em</td>
    <td>用于对文本内容进行强调，强调位置的不同通常会改变句子的含义</td>
    </tr>
    <tr>
        <td>del</td>
        <td>文档中已被删除的文本,与 ins 标签配合使用,描述文档中的更新和修正。</td>
    </tr>
    <tr>
        <td>ins</td>
        <td>定义已经被插入文档中的文本</td>
    </tr>
    <tr>
        <td>自然样式标签</td>
        <td>b - i - s - u</td>
    </tr>
</table>

**_一般情况尽量使用语义式标签，自然式标签单纯表现显示效果，语义式对浏览器更加友好。_**

### 图片与链接

#### 引用图片

```html
<img src='图片路径' alt='替换文本' title='鼠标悬浮提示文本' width='' height ='' />
```

* **_src 使用相对路径_**
* **_单独使用 width 或者 height 不改变图片形状_**

#### 超链接

```html
<a href='地址' title='提示文本' target = '打开方式' >
```

target="\_self" 默认值 在自身页面打开（关闭自身页面，打开链接页面）

target="\_blank" 打开新页面 （自身页面不关闭，打开一个新的链接页面）

#### 锚链接

1.先定义一个锚点

```html
<p id='top'>
```

2.超链接到锚点

```html
<a href='#top'>回到顶部</a>
```

#### 空链

```html
<a href='#>空链</a>
```

#### 压缩文件下载

```html
<a href='路径/压缩包.rar'>压缩包</a>
```

_*不推荐使用*_

#### 超链接优化写法

```html
<base target="_blank">  
```

让所有的超链接都在新窗口打开

### 特殊字符

参见[特殊字符表](/posts/901119866.html)

### 列表

#### 无序列表

```html
<ul type="">
    <li></li>    列表项
    <li></li>
    <li></li>
</ul>
```

* type="square"－＞小方块
* type="disc"－＞实心小圆圈
* type="circle"－＞空心小圆圈

####　有序列表

```html
<ol type="" start="">
    <li></li>    列表项
    <li></li>
    <li></li>
</ol>
```

* type="1,a,A,i,I" type 的值可以为 1,a,A,i,I
* start="number" 决定了开始的位置。

#### 自定义列表

```html
<dl>
    <dt></dt>    小标题
    <dd></dd>   解释标题
    <dd></dd>   解释标题
</dl>
```

### 音乐标签

```html
<embed src="xxx.mp3" hidden='true'>
```

hidden:隐藏播放按钮

### 滚动标签

```html
<marquee>text/img/picture</marquee>
```

属性:

* direction 控制滚动方向 默认从右向左
* scrollamount 控制文字滚动的速度
* loop 控制文字滚动的次数，默认的值是-1.也就是无限次滚动
* behavior 设置滚动的类型
  * "slide"，文字滚动到边界后就会停止，不会再继续滚动
  * "alternate" 文字滚动到边界后会反方向弹回来，并且来回滚动
  * "srcoll" 表示由一端滚动到来一端，会重复
