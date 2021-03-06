---
title: Hexo+Github搭建Blog
date: 2019-03-14
tags: Hexo
categories: Blog Setup
mathjax: false
copyright: true

---
本文将简略介绍利用Github和Hexo搭建本地Blog的方法。需要注意，请按照文中各部分给出的**链接**进行搭建，以免踩坑。本文框架为：

- 基本准备；
- 搭建流程；
- 配置Hexo完善Blog。
<!-- more -->

## 基本准备
1. 申请一个Github账号，并以<Github用户名>.github.io命名一个公开的repo；
2. 在电脑上安装git、Node.js之后安装Hexo，参见[Hexo官网](https://hexo.io/zh-cn/docs/index.html#安装-Node-js)。

## 搭建流程
1. 初始化Hexo，尝试Hexo基本操作，并编写第一篇文章，详细过程参见[Division By Zero](https://zeromath.github.io/2017/03/11/hexo-github/)；
2. 装载新主题[NexT](http://theme-next.iissnan.com/getting-started.html)（此过程中请务必在Blog根目录下进行）；
3. 发布文章到网上，并添加SSH KEY，参见[Division By Zero](https://zeromath.github.io/2017/03/21/hexo-github2/)（请注意区分Blog目录下的“_config.yml”和themes/next下的“_config.yml”）；
4. 配置NexT主题，添加个性化功能，例如：[主题风格](http://theme-next.iissnan.com/getting-started.html)、[搜索服务、添加标签、添加分类](https://zeromath.github.io/2017/03/21/hexo-github3/)、[评论功能](https://www.jianshu.com/p/57afa4844aaa)等。

## 配置Hexo完善Blog
### 对数学公式的支持
Hexo博客主要基于Markdown语言，而在Markdown语言中输入数学公式一个比较好的方法是使用[MathJax引擎](https://blog.csdn.net/xiahouzuoxin/article/details/26478179)。为了使博客支持MathJax，我们需要配置Hexo渲染MathJax中的数学公式，参见[简书教程](https://www.jianshu.com/p/7ab21c7f0674)和[Hexo博客使用MathJax](http://wangwlj.com/2017/09/21/markdown_mathjax/)。

插一句题外话，由于本地Markdown编译器对MathJax引擎的兼容度不尽人意，因此我选择在[StackEdit](https://stackedit.io/app#)上写md文档。

MathJax中的语法类似Tex，一些基本的语法参见[MathJax(Markdown中的公式)的基本使用语法](http://wangwlj.com/2017/10/08/mathjax_basic/)。

### 对图片支持
有时候博文中会配有图片或动图，因此我需要一个与md文件配套的文件夹来存放他们。这部分请参看[Division By Zero](https://zeromath.github.io/2017/03/22/hexo-github4/)。

### 对流程图支持
在Markdown中使用mermaid包，我们可以非常容易地画出流程图和顺序图。为了将这种方便延续到博客的写作中，我们需要配置Hexo来支持mermaid包。具体做法请参考[TY·Loafer](https://tyloafer.github.io/2018/04/21/hexo-mermaid/)和[hexo-filter-mermaid-diagrams](https://github.com/webappdevelp/hexo-filter-mermaid-diagrams)。其中，TY·Loafer的代码有些问题，请同时参考上面两个链接中的方法，并使用后者提供的代码。

### 文章置顶及折叠
要使文章置顶，需要装载新的Hexo模块并修改next中的设置，参见[Hexo文章置顶](https://blog.csdn.net/qwerty200696/article/details/79010629)。

要使文章折叠，可以在md文件的导语和正文之间添加：
```
<!-- more -->
```
md文件的一般格式如下：
```
---
title: XXX
date: 20XX-XX-XX
tags: 
categories: 
mathjax: (是否使用MathJax)
top: （文章是否置顶）
copyright: true
---
（导语）
<!-- more -->
（正文）
```
可以在`/scaffolds/post.md`文件中修改好上述默认格式，之后每一次`$ hexo new`即可。

### 添加统计功能
NexT主题中自带的busuanzi功能可以实现访客数与浏览数统计，参见[Hexo使用不蒜子统计功能](https://www.jianshu.com/p/089762f90e1c)。

### 增加版权信息
自己的劳动成果当然不想被他人窃取，在文章末尾添加版权信息是一种不错的保护自己的手段。参见[hexo的next主题个性化配置教程之20](https://segmentfault.com/a/1190000009544924#articleHeader12)。

### 文章加密访问
有些私密文章，设置一些密码也是必须的。这里有两个参考教程：[hexo的next主题个性化配置教程之20](https://segmentfault.com/a/1190000009544924#articleHeader12)和[Hexo文章简单加密访问](https://blog.csdn.net/Lancelot_Lewis/article/details/53422901)。根据第二个教程，建议将代码放在所有的`<meta>`标签之后。

## 发布/删除文章
### 发布文章
将写好的Markdown文件拖入`/Blog/source/_posts/`，之后运行
```
$ hexo generate  
$ hexo server（生成本地预览）
```

### 删除文章
在`/Blog/source/_posts/`中删除相关文件，之后运行
```
$ hexo clean  
$ hexo generate  
$ hexo server（生成本地预览）
```

### 草稿功能
有时候想在网站中删除相关文章，而不删除相关Markdown文件，可以将此文件存入到“草稿”中。
#### 创建草稿
```
$ hexo new draft <title>
```
这时，草稿将被保存在`/Blog/source/_drafts/`当中。

#### 预览草稿
草稿中的文件不会出现在网页中，但可以通过一下命令进行预览。
```
$ hexo server --draft
```
#### 发布草稿
运行以下代码，可将草稿中的文件移动到`/Blog/source/_posts/`当中。
```
$ hexo publish <title>
```

最后运行
```
$ hexo deploy
```
将文章部署到Github个人网站上。
（也可简单的使用`$ hexo d -g`实现部署过程）



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5MTExNDU0OF19
-->