--- 
title: "Bookdown中文书稿写作手册"
author: "汤银才"
date: "2021-07-21"
output: pdf_document
fontsize: 12pt
indent: yes
linestretch: 2
bibliography:
- book.bib
- packages.bib
biblio-style: gb7714-2015ay
biblatexoptions:
- refsegment=chapter
- gblocal=chinese
- gbnamefmt=lowercase
- gbnamefmt=familyahead
- gbtype=false
- maxbibnames=99
link-citations: yes
nocite: |
  @*
colorlinks: yes
lot: yes
lof: yes
geometry:
- a4paper
- tmargin=2.5cm
- bmargin=2.5cm
- lmargin=3.5cm
- rmargin=2.5cm
site: bookdown::bookdown_site
github-repo: tangyc8866.github.io/bookdown-tyc/
url: https://tangyc8866.github.io/bookdown-tyc/
description: bookdown写书体验非常好.
#documentclass: ctexbook
documentclass: krantz
---







# 前言 {.unnumbered} 


\indent
今年接了5本与贝叶斯近似计算包`INLA`相关的翻译书，将由高等教育出版社出版。在准备翻译的时候，我静下来思考了一下二个问题。一是互联网时代在兼顾图书质量的同时怎么充分考虑读者阅读体验？二是什么是当下最为成熟的图书写作工具？特别是与数据科学密切相关的统计类图书的写作与出版。书稿模板的选择成为首先要考虑的事。

在书稿模板的选择与测试过程中遇到了很多的坑，幸运的是逐个踩过来了，但从$\TeX$到`Rnw` (Sweave+R), 再到`Rmd` (Knitr + R), 最后到`Bookdown`, 共经历了4个模板。快速、高效、高质量是写书人追求的目标。目前来看`Bookdown`是最好的选择，因为它满足我模板选择的快速编辑、高效生成、高质量输出的要求。

这本小册子可视为一个写中文书稿的`Bokdown`模板，也是中文`Bookdown`写作的一本说明书，其中汇总了书稿中几大核心要素的写作技巧。我主要参考了三个模板`Bookdown`模板和三本电子书，罗列如下，在此一并对谢益辉、李东风等表示感谢。 

1. 谢益辉, [bookdown 中文范例](https://github.com/yihui/bookdown-chinese)

1. 谢益辉, [A bookdown example for Chapman & Hall books](https://github.com/yihui/bookdown-crc)

1. [bookdown-chapterbib](https://github.com/rstub/bookdown-chapterbib)

1. 谢益辉, bookdown: [Authoring Books and Technical Documents with R Markdown](https://bookdown.org/yihui/bookdown/), 2021-03-15.

1. 李东风，R语言教程，[第23章：用bookdown制作图书](https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/bookdown.html), 2020-12-28.

1. Yihui Xie, J. J. Allaire, Garrett Grolemund, [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/), 2020-12-14.




