---
layout: page
title: 如何写文档
author: Cloudhan
---

## 目录
{:.no_toc}

* ToC
{:toc}

---



## 基础使用

这是一个`Jekyll`的主题，它很简洁、很漂亮，适合撰写文章。你可以撰写自己的短文、诗歌、甚至小说、自传来发布，我一直有个写作的梦想，之所以喜欢这个主题，大致源于此吧！这里还是得感谢下`Ed`主题的发布者 `Alex Gil` 及其团队给了我们很好的体验。<br>
要想很好的使用`Ed`，除了熟悉基础的`markdown`语法，还需要会使用`git`,`rvm`, `bundle`, `jekyll 2.7.3`的基础指令和`Liquid`的语法知识。<br>
`Ed`的运行环境是`ubuntu`，相比`windows`环境运行更加稳定;所以手册里看到的终端命令和相关工具都是在`ubuntu 16.04 LTS`的环境中运行的。


如果你迫不及待已经想撰写Blog了，打开`blog`文件夹，右键选择`在终端打开`，或者`Ctrl+Alt+T` 打开终端：
~~~ bash
$ cd blog
$ rvm use 2.4.1@jekyll
$ subl .
~~~
写好Blog先要在本地启动`Jekyll`服务预览下，确保没有错误发生，本地`Firefox`浏览器地址为`127.0.0.1:4000`
~~~ bash
$ jekyll serve
~~~
发布到`Github`的服务器,需要注意的是：blog使用了`cloudhan.me`的域名，没有使用账户名（事实上账户名网站是我的技术blog），这是个项目网站，所以这里不是master分支：

~~~ bash
$ git status
$ git add .
$ git commit -m "first commit"
$ git push origin gh-pages
~~~

---

## 文章格式及命名规范

对于`Jekyll`的文档可以参考 [Jekyll中文网](http://jekyllrb.com.cn/) 或者`安道`的教程。我使用的纯文本编辑工具是`sublime-text3`，我确保它是个神奇的工具，非常方便好用。

撰写的blog文章在`_texts` 文件夹里，记住每篇文章命名规则是  `your-title.md` 。每篇文章的`YAML`顶部信息确保遵守如下规则：
~~~ yaml
---
layout: poem
title: "Cahier d'un retour au pays natal"
author: Cloudhan
---
~~~
---

## kramdown 语法

除了使用`markdown`原生的语法，主题使用`kramdown`拓展语法，主要就是对表格的支持，还包括脚注，词汇定义，缩写, 图片和视频等。可以参考[简书：让你的Markdown用起来得心应手](https://www.jianshu.com/p/d7d6da4b7c60)一文。

---

## 文章版式

`Ed`主题提供了三种不同的版式:`诗歌：poem`、`故事:narrative`和`戏剧：drama`。文章顶部的`YAML`信息`layout: page`定义了该布局。布局模板文件在`_layouts`文件夹中可以找到。使用这些布局将允许您根据您不同的写作需求调整样式，一些特殊指令是需要了解的。


诗歌中常用的行开始标记语法：

~~~ markdown
- Hold fast to dreams
- For if dreams die
- Life is a broken-winged bird
- That cannot fly.
- Hold fast to dreams
- For when dreams go
- Life is a barren field
- Frozen with snow.
~~~

行缩进的语法：

~~~ markdown
- {:.indent-3} But O heart! heart! heart!
- {:.indent-4} O the bleeding drops of red,
- {:.indent-5} Where on the deck my Captain lies,
- {:.indent-6} Fallen cold and dead.
~~~

这里 `-` 表示一行的开始;`{:.indent-3}` 表示缩进值，值得范围可以从1-10;`*` 包围则是使用斜体字，如： 

*这里是斜体字* 

--- 

## 脚注的使用

脚注的语法很简洁：行文中插入`[^fn2]`即可，注解处使用 `[^fn2]:XXX` 即可，可以实现相互跳转。


~~~ 
- O Captain! my Captain! rise up and hear the bells; 
- Rise up—for you the flag is flung—for you the bugle[^fn2] trills,

...

[^fn2]: The bugle is a small trumpet implicated in the military industrial complex.
~~~

多行脚注需要同样保持缩进：

~~~ 
[^fn3]:
	Ugh pinterest fixie cronut pitchfork beard. Literally deep 
	cold-pressed distillery pabst austin. 

	这是第二行注解：Typewriter 90's roof party poutine, kickstarter raw 
	denim pabst readymade biodiesel umami chicharrones XOXO. 
~~~

文章中某些标记并不一定使用数字，例如只使用一个`*` 符号，脚注尾部使用&#x21a9;&#xfe0e;返回标记处,
`HTML`可以提供方法：

~~~ html
... At this time, Anna,<sup><a href="#fn2" id="ref2">\*</a></sup> my intended wife, came on;

...

<sup id="fn2">*</sup> She was free. [&#x21a9;&#xfe0e;](#ref2)
~~~

---

## 块级引用

引用在`kramdown`的实现非常简单,其中的文字是引用内容。

~~~ 
> This is to certify that I, the undersigned, have given the bearer, my servant, full liberty to go to Baltimore, and spend the Easter holidays.
>
> Written with mine own hand, &c., 1835.  
> WILLIAM HAMILTON,
~~~

设想在一个`故事:narrative`的版式中，块引用`诗歌：poem`，语法是怎样的呢？

~~~
...
> - Two others oped their iron jaws,
> - And waved their children-stealing paws;
> - There sat their children in gewgaws;
> - By stinting negroes' backs and maws,
> - They kept up heavenly union.
> ^
> - All good from Jack another takes,
> - And entertains their flirts and rakes,
> - Who dress as sleek as glossy snakes,
> - And cram their mouths with sweetened cakes;
> - And this goes down for union.
{:.poetry}
~~~

这个`{:.poetry}`标记是告诉程序把上面的`-`行标记作为`诗歌：poem`版式处理，之所以需要声明是因为这段文字本身的版式是`故事:narrative`版式，以便程序正确调用。

---

## 页面模板

你已经知道，blog 文章都是放在`_text`文件夹，其他的页面模板（例如：`about`, `index`, `documentation`）则是在根目录下的。
你会注意到，模板文件有些是以`.html`而不是`.md`结尾。`Jekyll`中的所有模板文件都是`HTML`。虽然这些文件大多是用`HTML`编写的，但它们仍然包含`YAML`顶部信息和`Liquid`标签。
不同的地方是：`.html`文件不能使用`markdown`语法和扩展，但可以使用`Liquid`语句，同理`.md`结尾的文件不能含有`Liquid`语句。

---

## 目录表

`Ed`主题里可以建立三种目录表，第一个示例是主页中用`Liquid` 模板语言编写的文章目录， `{%raw%}{% %}{%endraw%}` 是逻辑表达式的写法， `{%raw%}{{ }}{%endraw%}` 只是输出内容，示例中是文章的标题。
<!--  `raw`-暂时停用标签处理以避免出现语法冲突。--> 

~~~ html
<div class="toc">
  <h2>Sample texts</h2>
  <ul class="post">
 
  {%raw%}{% for item in site.posts do %}{%endraw%}
      <li class="post-title">
      <a href="{%raw%}{{ site.baseurl }}{{ item.url }}{%endraw%}">
      	{%raw%}{{ item.title }}{%endraw%}
      </a>
    </li>
  {%raw%}{% endfor %}{%endraw%}
  </ul>  
</div>

~~~
第二个示例恰好就是本文件顶部应用的目录语法。这是`kramdown`的方式，`{:.no_toc}`的作用是告诉程序不要把`Contents`作为目录内容，下面的语句是把文中`markdown`标题自动生成目录内容放在`{:toc}`的位置。

~~~ markdown
## Contents
{:.no_toc}

* ToC
{:toc}
~~~
对于多章节的长篇文章，第三种方式更为适合，在`YAML`的顶部信息中写入目录，这种方式的好处是在阅读文章时可以通过侧边栏看到目录大纲，实现方便的章节跳转和返回。

~~~ yaml
toc:
- Title Page
- Preface
- Letter From Wendell Phillips
- Chapter I
- Chapter II
~~~

---

## 改变主题颜色和布局

如果你不喜欢`Ed`默认的颜色，可以在`default.html`版式中方便的调整和修改。只需要改变`bord`标签的 `class` 属性即可。详细参见:[Lanyon documentation](https://github.com/poole/lanyon#themes).

 - 侧边栏在右侧：`<body class="layout-reverse sidebar-overlay">`
 - 改变基本主题颜色：`<body class="theme-base-08">`

---





Cloudhan  
April 2018