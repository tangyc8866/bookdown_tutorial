# `Bookdown`中的文本参考 {#textref}

\indent
这是第\@ref(textref)章的内容, 讲述文本的标签与引用. [@xie2015; @R-base]

## 文本标签的设定与引用 {#sec7-1}

\indent
通过`(ref:label)`设定被引文本，其前后必须有空行与正文分开. 例如

```
(ref:foo) 我要被引用的**文本**. 

被引用的文本： (ref:foo) 
```
输出为

(ref:fooo) 我要被引用的**文本**. 

被引用的文本： (ref:fooo) 

## 文本引用场景 {#sec7-2}

\indent
在`Bookdown`中文本引用主要用于图形与表格的题图(caption)上， 见第\@ref(figures)章和第\@ref(tables)章的例子. 

\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]

