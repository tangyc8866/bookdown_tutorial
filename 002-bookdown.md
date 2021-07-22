# `bookdown`速览 {#bookdown} 


\indent
这是第\@ref(bookdown)章的内容，概要性地讲解基于`bookdown`拓展包进行图书排版的整体思路与实现方式. [@xie2015; @R-base]


## 关于`bookdown` {#sec2-1}

\indent
`bookdown`扩展包(https://github.com/rstudio/bookdown) 是继`knitr`和`rmarkdown`扩展包之后， 另一个增强`markdown`格式的扩展， 使得`Rmd`格式可以支持公式、定理、图表、文献自动编号和引用等适用于编写书籍的功能。 在`bookdown`的管理下一本书的内容可以按章节分解成多个`Rmd`文件， 其中可以包含可执行的`R`代码， `R`代码生成的统计汇总结果、表格、图形可以自动插入到生成的内容中， 表格和图形可以是浮动排版的。书的输出格式包括支持`gitbook`格式的网页图书， 也可以经$\LaTeX$编译器转换的`PDF`图书，还 可以生成`ePub`等格式的电子书。建议使用`RStudio`集成环境来编辑、管理和生成这样的图书，可通过其内建的一键式编译整本书的插件(`build`)实现。

## 快速排版的思路 {#sec2-2}

1. 由`rmarkdown`完成整个书稿的写作;

1. 由`_output.yml`完成不同形式呈现的书稿的设计，其中`bookdown::gitbook`负责`html`形式的`gitbook`, `bookdown::pdf_book` 负责`pdf`形式的电子书（由$\TeX$支持)；`bookdown::epub_book`负责`epub`电子书. 部分针对书稿简单设置可放在`index.Rmd`文件的`yml`头部(具体放在前面两组三个短线`---`之间);

1. 书稿按章节进行拆分，借助`js`支持的`html`快速生成书稿的初稿，最后再进行整合，根据需要通过`Build`插件完成`gitbook`, `pdf_book`, `epub`的构建;

1. 借助`mathjax`处理数学公式的渲染;

   尽快可通过联网由`cdn`上的`mathjax.js`进行渲染，但速度随因公式的增加，渲染变得很慢，甚至出错。`mathjax`的本地化是提速的主要解决方案. 详见第\@ref(mjx)章介绍； 

1. 重点做好章节、数学公式、表格、图形、定理、文献等浮动对象的处理，在编写过程中及时做好标签设定与引用，见\@ref(sec2-6)节的汇总表格及后续各章的介绍与示例. 

## 书的基本设置 {#sec2-3}

\indent
一本用`bookdown`管理的书， 一般放置在某个子目录下，并作为一个`RStudio`项目(project)用`RStudio`管理。该目录中的所有的文本文件都要使用`UTF-8`编码。

### `index.Rmd`文件 

\indent
 一本`bookdown`书， 一般都需要有一个`index.Rmd`文件， 这是最后生成的网站的主页的原始文件. 这个文件的开始是`YAML`元数据部分, 进行全书的有关设置，包括标题、作者、日期及影响全书的一些选项等，放在三个减号组成的两行之间。然后写一些这本书的说明，如书的前言部分。`index.Rmd`中`YAML`元数据部分的一个例子如下：
```
title: "bookdown书稿模板"
author: "汤银才"
date: "2021-07-21"
documentclass: book
bibliography: [myrefs.bib]
biblio-style: apa
link-citations: yes
site: bookdown::bookdown_site
description: "bookdown写书体验非常好."
```

注意: 

1. `site`选项很重要， 一定要有， `site: bookdown::bookdown_site`使得`RStudio`能辨认这是一个`bookdown`图书项目， 从而为其生成一键编译的`build`快捷方式；

2. 在`bookdown`项目中与`index.Rmd`同级的所有`.Rmd`文件都自动作为书的一章，其好处是作者可以任意地增删章节，编译整本书时将按照文件名的字典序依次进行。实际上， 也可以在`_output.yml`文件中设置一项`rmd_files`， 列出所有需要作为一章的文件，并以列出次序编译；

3.  在`index.Rmd`的元数据中也可以指定一些$\LaTeX$的选项, 例如
```
fontsize: 12pt
indent: true
linestretch: 2.0
link-citations: yes
colorlinks: yes
lot: true
lof: true
geometry:
- a4paper
- tmargin=2.5cm
- bmargin=2.5cm
- lmargin=3.5cm
- rmargin=2.5cm
```

### `_bookdown.yml`文件

\indent
一个`bookdown`图书项目除了`index.Rmd`文件之外，还有一些设置文件从`index.Rmd`文件的元数据部分抽离出来。 一个是`_bookdown.yml`文件, 它存放与整本书的处理有关的`YAML`元数据。 例如
```
book_filename: "bookdown-template"
new_session: yes
language:
  label:
    fig: "图 "
    tab: "表 "
    thm: '定理'
    def: '定义'
    exm: '例'
    proof: '证明: '
  ui:
    chapter_name: ["第 ", " 章"]
```
其中`new_session: true`设置很重要，这使得每一个`Rmd`文件中的`R`程序都在一个单独的`R`会话中独立地运行，避免了不同`Rmd`文件之间同名变量和同名标签的互相干扰。 `book_filename`是最终生成的`PDF`图书或者`ePub`电子书的主文件名。 `language`下可以定制一些与章节名、定理名等有关的名称。

### `_output.yml`文件

\indent
另一个设置文件是`_output.yml`， 用于图书输出格式的设置^[这部分内容也可以包含在`index.Rmd`的元数据部分], 本小删子的`_output.yml`文件内容如下
```
bookdown::gitbook:
  css: css/style.css
  split_by: chapter
  includes:
    in_header: _header.html
  config:
    toc:
      collapse: subsection
      scroll_highlight: yes
      before: |
        <li><a href="./">bookdown排版模板</a></li>
      after: |
        <li><a href="https://bookdown.org" target="blank">本书由 bookdown 强力驱动</a></li>
    download: [pdf, epub]
    edit: https://github.com/yihui/bookdown-chinese/edit/master/%s
    sharing:
      github: yes
      facebook: no
  pandoc_args: [ "--csl", "apa-6th-edition-no-ampersand.csl" ]
bookdown::pdf_book:
  includes:
    in_header: latex/preamble.tex
    before_body: latex/before_body.tex
    after_body: latex/after_body.tex
  keep_tex: yes
  dev: "cairo_pdf"
  latex_engine: xelatex
  citation_package: biblatex
  template: latex/template.tex
  toc_depth: 3
  toc_unnumbered: no
  toc_appendix: yes
  quote_footer: ["\\begin{flushright}", "\\end{flushright}"]
  pandoc_args: [ "--top-level-division=chapter" ]
bookdown::epub_book:
  stylesheet: css/style.css
  pandoc_args: [ "--csl", "apa-6th-edition-no-ampersand.csl" ]
```
它分别对`gitbook`、`pdf_book`和`epub_book`三种输出格式设置了一些输出选项。其中一些选项是通过文件形式给出设置的，我们再补充说明一下。

   1. `style.css`是自定义的CSS显示格式，在`gitbook`和`epub_book`中使用;

   2. `_header.html`是插入了一部分个性化的`HTML`代码，其内容将出现在每个生成的`HTML`文件的`head`部分。我们在此文件中给出了使用本地的`Mathjax`实现数学公式离线显示的设置，内容为
  
  ```
  <script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    jax: ["input/TeX","output/SVG"],
    extensions: ["tex2jax.js","MathMenu.js","MathZoom.js"],
    TeX: {
      Macros: {
        bm: ["{\\boldsymbol #1}",1],
      }, 
      extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"]
    }
  });

  </script>
  <script type="text/javascript"
    src="http://127.0.0.1/MathJax/MathJax.js">
  </script>
  ```
  
   其中`http://127.0.0.1/MathJax/`是本地服务器上`Mathjax`的位置。有关`Mathjax`的本地安装与启动可参考第\@ref(mjx)章的介绍;

   3. `apa-6th-edition-no-ampersand.csl` 是`gitbook`和`epub_book`处理文献使用的风格文件;

   4. `preamble.tex`是处理(编译)`bookdown`文件经`pandoc`转化生成的`tex`文件时导言区需要额外的宏包和设置;

   5. `before_body.tex` 是`tex`书稿类正文前面的设置，最基本的是
   
   ```
    \frontmatter
   ```

   6. `after_body.tex` 是`tex`书稿类正文之后的设置，最基本的是
    
   ```
   \backmatter
   ```

    7. `template.tex` 是针对`bookdown`编译经`pandoc`转化生成的`tex`文件时的模板，由它生成供`latex_engine`指定的编译方式(`xelatex`)编译的`tex`文件. `index.Rmd`及`_output.yml`中的设置会嵌入到这个模板中，生成完整的单文档`tex`源文件.   

其他选项说明：

  1. `split_by: chapter`: 按章分割书稿；

  2. `collapse: subsection`: 目录中隐藏子节(仅显示二级标题)；
  
  3. `scroll_highlight: yes`: 目录滚动时高亮显示，便于定位；

  4. `keep_tex: yes`: 保留中间生成的`tex`源文件，便于查错；

  5.  `dev: "cairo_pdf"`: 使用`cairo_pdf()`生成 $\LaTeX$ 编译需要的图片文件;

  6. `latex_engine: xelatex`: `TeX`文件的排版引擎为$Xe\LaTeX$, 针对`UTF-8`编码;

  7. `citation_package: biblatex`: 文献引用库指定为`biblatex`, 另一个为`natbib`;

  8.  `toc_depth: 3`: 目录提取至三级标题;

  9.  `toc_unnumbered: no`: 指定目录编号;

  10. `toc_appendix: yes`: 附录添加到目录中. 



## 章节结构 {#sec2-4}

\indent
如前所述, 除了`index.Rmd`文件， 项目中每个`.Rmd`文件都作为一章，其第一行是以一个`#`号和空格开头的一级标题。

每一章可以有若干节与子节，分别用`markdown`的二级标题(二个`#`开始)和三级标题(三个`#`开始)编写。`bookdown`的章、节、子节标题单独成一行，其后可以添加标签, 章节的标签是标题后加空格，然后是大括号内以`#`号开头的标签， 如
```
# 引言 {#intro}

## 关于bookdown {#bookdown}
```

`bookdown`中有二个特殊的标题：

1. 部分

   内容相近的章节可以作为一个“部分”。 为此，在一个部分的第一个章节文件的章标题前面增加一行， 以`# (PART)` 开头， 以`{-}`结尾，例如
   
```
   # (PART) bookdown中的浮动对象 {-}
```

2. 附录

   一本书的最后可以有附录， 附录的章节将显示为`A.1`, `B.1`这样的格式。 为此， 在附录章节的第一个文件开头加如下的第一行标题行：
   
```
   # (APPENDIX) 附录 {-}

   # biblatex介绍 {#biber}
```


## 书的编译 {#sec2-5}


(ref:fig2p1) R Bookdown编译界面.


\indent
在`index.Rmd`或者`_bookdown.yml`中设置`site: bookdown::bookdown_site`后， `RStudio`就能识别这个项目是一个`bookdown`项目， 这时`RStudio`会有一个`Build`按钮，其中有`Build book`快捷图标， 从下拉菜单中选择一个输出格式（包括`gitbook`、`pdf_book`、`epub_book`）， 就可以编译整本书(见图\@ref(fig:fig2-1))。
<div class="figure">
<img src="./figures/Rbookdown-compile.jpg" alt="(ref:fig2p1)" width="85%" />
<p class="caption">(\#fig:fig2-1)(ref:fig2p1)</p>
</div>

经`build`编译生成的图书默认保存在`_book`子目录中^[可以在`_bookdown.yml`中设置`output_dir`项改变图书保存的子目录.]。

1. 对`gitbook`格式(即`HTML`网页格式)， 编译完成后会弹出一个预览窗口， 点击“Show  in new window ”按钮可以将内容在操作系统默认的网络浏览器中打开。我们也可以用其他浏览器(建议使用Google chrome浏览器)打开`_book`子目录中的`index.html`文件来查看`gitbook`格式的图书。

2. 对于`pdf_book`格式，如果成功编译^[需要$\LaTeX$支持，建议安排`TeXLive`，也可以仅安装谢益辉为`rmarkdown`开发的`tinytex`]， 也会弹出一个`PDF`预览窗口。 可以在`_book`子目录中找到这个`PDF`文件。

3. 对于`epub_book`格式，如果成功编译，会在操作系统默认的`ePub`软件(如苹果电脑的`book`)中打开,并在`_book`子目录中找到这个`ePub`文件。

## 浮动对象标签与引用汇总 {#sec2-6}


| 浮动对象     |  标签设置     |  引用格式          |
| -----------:|:-------------|:------------------|
| 标题         | `(# label)`   | `\@ref(label)`     |  
| 公式         | `(\#eq:label)`| `\@ref(eq:label)`  |
| 图形         | `label="label"`| `\@ref(fig:label)`|
| 表格         | `label="label"`| `\@ref(tab:label)`|
| 定理         | `label="label"`| `\@ref(prefix:label)`|
| 文本         | `(ref:label)` |  `` `(ref:label)` ``   |
| 文献         | `biblabel`    | `@biblabel`        |


注：

1. 定理泛指定理类，包括定理(thm)、引理(lem)、推论(cor)、命题(prp)、设想(cnj)、定义(def)、例子(exm)、习题(exr)等, 其中括号中是引用时的前缀(prefix);

1. 文本标签在单独一行中设定，可用在表格与图形的`caption`中引用，即在 `fig.caption`, `tab.caption`选项的设置中引用； 

1. 定理类环境标签前缀的汉化可在`_bookdown.yml`中通过`language`进行^[图形与表格也可同理汉化]，例如

```
language:
  label:
    fig: "图 "
    tab: "表 "
    thm: '定理'
    def: '定义'
    exm: '例'
```
    


\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]


