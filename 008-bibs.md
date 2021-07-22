# `Bookdown`中的文献排版 {#bibs}

\indent
这是第\@ref(bibs)章的内容，讲解文献库的建立、文献格式与排版方法. [@xie2015; @R-base]

## 文献库建立样例 {#sec8-1}

\indent
根据文献的类型，文献库的格式有14种类型，它们由`title`,`author`, `journal`,`address`等域构成. 最为常见的文献类型是论文(`article`)和图书(`book`), 它们的格式如下
```
    @article{CitekeyArticle,
      author   = "P. J. Cohen",
      title    = "The independence of the continuum hypothesis",
      journal  = "Proceedings of the National Academy of Sciences",
      year     = 1963,
      volume   = "50",
      number   = "6",
      pages    = "1143--1148",
    }
```

```
    @book{CitekeyBook,
      author    = "Leonard Susskind and George Hrabovsky",
      title     = "Classical mechanics: the theoretical minimum",
      publisher = "Penguin Random House",
      address   = "New York, NY",
      year      = 2014
    }
```
其余类型参见网页:[The 14 BibTeX entry types](https://www.bibtex.com/e/entry-types/)。 
文献库通过`BiBTeX`或`BiBer`的运行生成文献目录(bibliography).


## 文献风格  {#sec8-2}

\indent
不同的期刊、书集对文献目录中参考文献的呈现方式有不同的要求，`BiBTeX`是通过风格(style)文件来控制(配合宏包`natbib`使用), `BiBer`是通过选项来控制(配合`biblatex`使用). 

文献呈现的风格分为作者-日期格式(author-date style)和数字格式(numeric)。作者-日期格式共有141个式样，其中最为常用的式样有2个，即`alpha`和`apalike`。 数据格式共88个式样，其中有8类是标准式样，也是最常用的式样，即`abbrv`, `acm`,`ieeetr`,`plain`,`siam`, 和`unsrt`。这些式样的具体形式与介绍见[](https://www.bibtex.com/styles/)

中文的文献排版根据国标GB/T77114-2015的规范，对文献的类型要求提供文献的标识代码，共有18个，例如图书用`M`标识，期刊论文用`J`标识。

## 中文文献风格的设置  {#sec8-3}

\indent
基于`BiBTeX`, 中文文献通过宏包`gbt7714`实现^[详见 https://github.com/87ouo/gbt7714-bibtex-style 说明]，兼容宏包`natbib`，在$\LaTeX$中使用方法如下：

1. 在导言区调用宏包 `gbt7714`；

1. 在正文中 `\cite{}`等引用文献；

1. 使用 `\bibliographystyle{}` 选择参考文献表的样式；

1. 使用 `\bibliography{}` 命令生成参考文献表;

1. 编译生成带文献的pdf文件，基于`xelatex`引擎的编译方式如下(`foo.tex`为文件名)

```
	xelatex foo.tex
	bibtex foo
	xelatex foo.tex
	xelatex foo.tex
```	



基于`BiBer`, 中文文献通过宏包`biblatex-gb7714-2015` 实现^[详见 https://github.com/hushidong/biblatex-gb7714-2015]，兼容宏包`biblatex`。本质上`biblatex-gb7714-2015` 是个式样宏包，依附于宏包`biblatex`, 通过式样选项使用. 在$\LaTeX$中使用方法如下：

1. 在导言区调用宏包 `biblatex`, 并设定文献样本和， 例如；

    - 使用顺序编码制：
	```
	\usepackage[backend=biber,style=gb7714-2015]{biblatex}
	```
    - 使用著者-出版年制^[尽管后端(`backend`)可以使用`bibtex`, 但不建议使用.]：

   ```
	\usepackage[backend=biber,style=gb7714-2015ay]{biblatex}
   ```

1. 在`\begin{document}`加载参考文献库，命令为`\addbibresource{}`


1. 在正文中 `\cite{}` 等引用文献；

1. 在需要出现文献目录的地方使用 `\printbibliography`，可通过`title`, `heading`, `segment`选项对输出进行控制;

1. 编译生成带文献的`pdf`文件，基于`xelatex`引擎的编译方式如下(`foo.tex`为文件名)

```
	xelatex foo.tex
	biber foo
	xelatex foo.tex
	xelatex foo.tex
```	


## 文献库的建立工具  {#sec8-4}

- Zotero

- JabRef


\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]

