---


---

<hr>
<p>title: Hexo+Github搭建Blog<br>
date: 2019-03-14<br>
tags: Hexo<br>
categories: Blog Setup<br>
mathjax: false</p>
<hr>
<p>本文将简略介绍利用Github和Hexo搭建本地Blog的方法。需要注意，请按照文中各部分给出的<strong>链接</strong>进行搭建，以免踩坑。本文框架为：</p>
<ul>
<li>基本准备；</li>
<li>搭建流程；</li>
<li>配置Hexo完善Blog。</li>
</ul>
<!-- more -->
<h2 id="基本准备">基本准备</h2>
<ol>
<li>申请一个Github账号，并以&lt;Github用户名&gt;.github.io命名一个公开的repo；</li>
<li>在电脑上安装git、Node.js之后安装Hexo，参见<a href="https://hexo.io/zh-cn/docs/index.html#%E5%AE%89%E8%A3%85-Node-js">Hexo官网</a>。</li>
</ol>
<h2 id="搭建流程">搭建流程</h2>
<ol>
<li>初始化Hexo，尝试Hexo基本操作，并编写第一篇文章，详细过程参见<a href="https://zeromath.github.io/2017/03/11/hexo-github/">Division By Zero</a>；</li>
<li>装载新主题<a href="http://theme-next.iissnan.com/getting-started.html">NexT</a>（此过程中请务必在Blog根目录下进行）；</li>
<li>发布文章到网上，并添加SSH KEY，参见<a href="https://zeromath.github.io/2017/03/21/hexo-github2/">Division By Zero</a>（请注意区分Blog目录下的“_config.yml”和themes/next下的“_config.yml”）；</li>
<li>配置NexT主题，添加个性化功能，例如：<a href="http://theme-next.iissnan.com/getting-started.html">主题风格</a>、<a href="https://zeromath.github.io/2017/03/21/hexo-github3/">搜索服务、添加标签、添加分类</a>、<a href="https://www.jianshu.com/p/57afa4844aaa">评论功能</a>等。</li>
</ol>
<h2 id="配置hexo完善blog">配置Hexo完善Blog</h2>
<h3 id="对数学公式的支持">对数学公式的支持</h3>
<p>Hexo博客主要基于Markdown语言，而在Markdown语言中输入数学公式一个比较好的方法是使用<a href="https://blog.csdn.net/xiahouzuoxin/article/details/26478179">MathJax引擎</a>。为了使博客支持MathJax，我们需要配置Hexo渲染MathJax中的数学公式，参见<a href="https://www.jianshu.com/p/7ab21c7f0674">简书教程</a>和<a href="http://wangwlj.com/2017/09/21/markdown_mathjax/">Hexo博客使用MathJax</a>。</p>
<p>插一句题外话，由于本地Markdown编译器对MathJax引擎的兼容度不尽人意，因此我选择在<a href="https://stackedit.io/app#">StackEdit</a>上写md文档。</p>
<p>MathJax中的语法类似Tex，一些基本的语法参见<a href="http://wangwlj.com/2017/10/08/mathjax_basic/">MathJax(Markdown中的公式)的基本使用语法</a>。</p>
<h3 id="对图片支持">对图片支持</h3>
<p>有时候博文中会配有图片或动图，因此我需要一个与md文件配套的文件夹来存放他们。这部分请参看<a href="https://zeromath.github.io/2017/03/22/hexo-github4/">Division By Zero</a>。</p>
<h3 id="对流程图支持">对流程图支持</h3>
<p>在Markdown中使用mermaid包，我们可以非常容易地画出流程图和顺序图。为了将这种方便延续到博客的写作中，我们需要配置Hexo来支持mermaid包。具体做法请参考<a href="https://tyloafer.github.io/2018/04/21/hexo-mermaid/">TY·Loafer</a>和<a href="https://github.com/webappdevelp/hexo-filter-mermaid-diagrams">hexo-filter-mermaid-diagrams</a>。其中，TY·Loafer的代码有些问题，请同时参考上面两个链接中的方法，并使用后者提供的代码。</p>
<h3 id="文章置顶及折叠">文章置顶及折叠</h3>
<p>要使文章置顶，需要装载新的Hexo模块并修改next中的设置，参见<a href="https://blog.csdn.net/qwerty200696/article/details/79010629">Hexo文章置顶</a>。</p>
<p>要使文章折叠，可以在md文件的导语和正文之间添加：</p>
<pre><code>&lt;!-- more --&gt;
</code></pre>
<p>md文件的一般格式如下：</p>
<pre><code>---
title: XXX
date: 20XX-XX-XX
tags: 
categories: 
mathjax: (是否使用MathJax)
top: （文章是否置顶）
---
（导语）
&lt;!-- more --&gt;
（正文）
</code></pre>
<h2 id="发布删除文章">发布/删除文章</h2>
<h3 id="发布文章">发布文章</h3>
<p>将写好的Markdown文件拖入<code>/Blog/source/_posts/</code>，之后运行</p>
<pre><code>$ hexo generate  
$ hexo server
</code></pre>
<h3 id="删除文章">删除文章</h3>
<p>在<code>/Blog/source/_posts/</code>中删除相关文件，之后运行</p>
<pre><code>$ hexo clean  
$ hexo generate  
$ hexo server
</code></pre>
<h3 id="草稿功能">草稿功能</h3>
<p>有时候想在网站中删除相关文章，而不删除相关Markdown文件，可以将此文件存入到“草稿”中。</p>
<h4 id="创建草稿">创建草稿</h4>
<pre><code>$ hexo new draft &lt;title&gt;
</code></pre>
<p>这时，草稿将被保存在<code>/Blog/source/_drafts/</code>当中。</p>
<h4 id="预览草稿">预览草稿</h4>
<p>草稿中的文件不会出现在网页中，但可以通过一下命令进行预览。</p>
<pre><code>$ hexo server --draft
</code></pre>
<h4 id="发布草稿">发布草稿</h4>
<p>运行以下代码，可将草稿中的文件移动到<code>/Blog/source/_posts/</code>当中。</p>
<pre><code>$ hexo publish &lt;title&gt;
</code></pre>

