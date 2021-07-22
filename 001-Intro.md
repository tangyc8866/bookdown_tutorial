\mainmatter

# 引言 {#intro} 

\indent
这是第\@ref(intro)章的内容，回顾中国图书发展的历史及最新趋势. [@xie2015; @R-base]，


## 中国图书出版的变化 {#sec1-1}

\indent
中国的图书出版经历一些折腾，方正系统一度非常流行，但现在看来是非常失败的，主要是它在解决公式排版的同时没有解决便利性，其本质上想实现在其自创的中文系统中将$\TeX$命令做一个映射以实现数学公式排版，同时完成格式的定制。

中国学术界也经历了一些折腾，如中科院张林波研究员等开发的`CCT`系统和华东师范大学肖刚与陈志杰等老师开发的天元系统，它们是$\TeX$系统汉化版，较好地解决了汉字生成与调用，但因没有考虑普适性或可拓展性而像方正系统一样随着`CJK`的逐渐成熟而逐渐被抛弃，均退出了历史舞台。而同期中科院吴凌云博士等在普及$\TeX$的同时开发的$\TeX$中文套餐$C\TeX$相当成功，主要是针对汉字排版的`ctex`宏包，并对三个主流的文档类`book`, `article`, `report`进行了定制，推出了相应的中文文档类`ctexbook`, `ctexart`, `ctexrep`, 由此避免了传统的基于`CJK`宏包需要的大幅定制，同时保证了与原有$\TeX$系统的兼容性。这样我们始终可以使用跨平台的`TeXLiVe`进行排版或各类模板的开发，例如各个出版社的图书模板、各个期刊的模板、各高校的硕士和博士毕业论文模板等。

$\TeX$的出现^[是伟大的`Knuth`创造了排版的奇迹]，而且始终屹立不倒的原因是什么？ 第一个原因是它解决了一个`Word`之类文字编辑系统的痛点，即从所见所得(WYSIWYG, What you see is what you get)到所想所得(WYTIWYG), 即通过一些$\TeX$命令集构成一个完整的编程语言，由它完成一个封闭的体系，具有类似`C`语言一样非常强大的开发功能，由此形成了后来的`latex`, `miktex`, `latex2.09`, `luatex`, `xetex`等$\TeX$编译引擎，它们在充分利用电脑系统资源的同时实现高质量输出需要的精度。

$\TeX$屹立不倒的另一个原因是浮动对象的处理，即包括公式，表格、图形、页码、章节、文献、定理等的标签化与引用，实现文档内部的自由跳转，结合`Acrobat Reader`这样强大的`pdf`阅读器的支持，使得读者的阅读体验得到大幅改善，并为图书的电子化奠定了基础。


随着数据科学这一新兴学科的出现，开源的`R`和`Python` (还有正在逐步流行的`Julia`)编程语言越来越强大。 为了增加这类图书的可读性，需要将代码较完整地呈现在读者面前，并且要求代码的即时可复现能力，即数据的变化，其分析的结果(包括图形和表格)也随之发生变化。这就是现在逐步流行的文学化编程(`literate programming`), 它实现上最早也是$\TeX$的鼻祖Knuth提出的, 后来被谢益辉得到重视并广泛推广，并通过`Rstudio`传递给`R`的用户。我们姑且把这种将写作与数据分析相结合的统计分析称为文学化统计编程(`literate statistical programming`), 在为数据科学爱好者带来便利的同时也通过`Bookdown`为图书的写作和电子化带来了极大的好处，越来越多的网页版电子书出现在(https://bookdown.org/)和(https://github.com/)等网站上。

现在写书选择什么类型的模板，下面我们来作进一步的探索与比较。

## 统计类图书的核心要素 {#sec1-2}
  
\indent
统计类图书的排版除普通图书的页面及文字风格等静态元素外，核心要素体现在浮动的对象上，使得图书的阅读体验更好地发挥出来，即在不同页面之间快速切换、跟踪、搜索，必要的`R`和`Python`代码以语法高亮方式显示。
  
  1. **章节标题**是浮动的，最主要用于书签的生成; 
  
  2. **公式**是浮动的，这是数学、统计等理科书的特点，公式引用必不可少;
  
  3. **图形**是浮动的，统计图形作为可视工具，在说明数据或展示分析结果时经常会引用相应的图形;
  
  4. **表格**是浮动的，通常是原始数据或统计分析的结果以表格形式展示出来，它们可能被多次在不同的章节中引用;
  
  5. **定理**是浮动的, 这里定理是指与之相关的一大类，包括常用的定理、引理、推论、命题、例子等，它们在文中也会被反复引用; 
  
  6. **文本**可以设置浮动标签后被引用，最为常见的是图形与表格的题图(caption)通过文本方式来引用;
  
  7. **文献**是浮动的，这在是谈及前人的已有工作、成果比较或进行综述时经常要引用大量已经发表的论文、图书、会议报告等.
  
$\TeX$有一套成熟的浮动对象的排版方式，通过给浮动对象打标签(label)，然后引用(ref), `Bookdown`思路一样，但比$\TeX$的处理稍复杂些(可能因不习惯引起)。我们在后面章节中分别举例说明。


## 统计数据分析类图书模板的选择 {#sec1-3}

\indent
统计数据分析类图书既有理论或原理的讲解，又会有一些案例分析，包括这些案例分析实现的代码。我们可以考虑的模板主要有三种类型。

### 基于纯 $\TeX$ 模板 {#sec1-3-1}

\indent
全世界90\%的书是由$\TeX$排版的，包括硕士和博士毕业论文模板，这要感谢鼻祖Knuth！开源成就了$\TeX$!

如果仅仅是统计理论方面的书集，这显然是最好的选择，因为高质量公式的排版离不开$\TeX$. 基于$\TeX$的排版存在三个明显的缺陷或不足:

  1. 大量的$\TeX$命令需要记忆;
  
  1. 对于代码的排版非常不便，特别是`R`或`Python`代码执行后的输出，尤其是图形与表格;

  1. 代码以`listing`等包来呈现, 无法实时呈现代码运行的结果，不符合文学化编程的要求.
  
### `R`markdown与$\TeX$的结合 {#sec1-3-2}

\indent
数据科学时代更注重文学化统计编程，**代码伴随**是这类图书的特点，自Springer出版`R`系列统计图书后，这种风格成为新趋势，大大方便了数据科学爱好者“便学习便练习”的学习方式。

针对代码伴随，早期对这类图书有二个解决方案：

  1. Sweave/knitr + `R`
  
本质上它是在 $\TeX$ 嵌入`R`代码块，并由`R`在后台运行后将结果也嵌入到$\TeX$中，再由$\TeX$的编译引擎生成`pdf`。这个方案的基本沿用$\TeX$的方式，它仅解决了上面提到的第二个问题。在数据科学时代，报告的快速生成成为新的要求，效率优先！随着`knitr`的出现`Sweave`退出舞台.
  
  2. `Rmarkdown` + `Mathjax`/$\TeX$
  
  `Markdown`作为一种轻量级的标记语言成为网页作为文字主要载体的互联网时代首先的写作工作，但它显然不适合数学与统计类论文或图书的撰写，但`knitr`和`pandoc`的出现使不同风格的内容整合与转换成为可能，而不同风格的内容各有善长的工具实现，作为统计类专业论文或图书类文档主要的内容有：
  
  a. 文字， 由markdown完成
  
  b. 公式，由$\TeX$完成 
  
  c. 代码，由`R` (或Python) 完成
  
要说明的是，在网页端，$\TeX$的实现可由`Mathjax`来完或渲染(转化或生成标准的公式)，见第\@ref(formulas)章说明。

随着`Rstudio`的越来越成熟与强大（得益于许多优秀包的出现，如`knitr`, `kableExtra`）, `Rstudio`不仅是一个很好的代码编辑器(`Eidtor`), 也是一个非常好的集成开发环境(`IDE`)，同时正在成为一个非常优秀的论文、幻灯片及图书等撰写与出版系统(`PUB`)。后者的基本流程是

  1. 由`rmd`文件通过`knitr`完成初步集成
  
  1. 由`pandoc`完成由`rmd`向`md`的转化与融合
  
  1. 由`pandoc`完成由`md`转化为$\TeX$, 并由`laTeX`编译生成`pdf` (形式多样!)
  
  1. 或由`pandoc`由`md`转化为`html`, 其中的数学公式由`Mathjax`完成渲染. 
  
###  `Rmarkdown`向`Bookdown`过渡 {#sec1-3-3}

\indent
在科技高度发达的互联系时代，读者使用的媒介基本有三类：较为专业的电脑，较为轻便的平板(电脑)和全功能的智能手机。前者以`pdf`类图书为主呈现给读者，同时可以完成标注等工作；后者以文字型的电子图书为主，消磨时间为主；而平板的使用者逐渐成为电子类图书的新势力，包括`pdf`和`epub`之类的电子书。
`Bookdown`注重不同类型读者的媒体使用的差异，并很好地实现统一编写与差异化输出。目前`Bookdown`可以生成三类图书:

  1. `gitbook`，可自由出版在`git pages`上
  
  2. `epub`, 发表到大量的电子图书平台上
  
  3. `pdf`, 正规的图书出版公司以电子或纸质形式出版
  



\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]


