# Bookdow中 的章节标题 {#sections} 

\indent
我们在第\@ref(sections)章讲述章节标题的设置、标签与引用. [@xie2015; @bookdown2016]

## 章节标题 {#sec3-1}

\indent
章节标题用遵从`markdown`的规则，用`#`设置，

- 一级标题用一个 `#`, 在bookdown中表示`章`, 相当于$\TeX$中的`\chapter{}`

- 二级标题用二个 `#`, 在bookdown中表示`节`, 相当于$\TeX$中的`\section{}`

- 三级标题用三个 `#`, 在bookdown中表示`子节`, 相当于$\TeX$中的`\subsection{}`

还可以有更深的标题.

## 章节标题标签的设定与引用 {#sec3-2}

\indent
章节标题标签可在标题后用 `{#label}`来设定，引用方式为`\@ref(label)`. 例如


```r
第\@ref(sections)章\@ref(sec3-2)节讨论标题标签的设定与引用.
```

显示为：

第\@ref(sections)章\@ref(sec3-2)节讨论标题标签的设定与引用.



\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]

