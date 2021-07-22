# `Bookdown`中的公式与定理 {#formulas}

\indent
这是第\@ref(formulas) 章的内容, 讲述浮动对象定理与公式的标签与引用.  [@xie2015; @bookdown2016]

## 公式标签的设定 {#sec4-1}

\indent
`Rmarkdown`中公式除了无标号的公式(用一对`$$`实现)，可以使用`LaTeX`中的`equation`环境, 尽管无法实现类似的WYSIWYG, 但可设置标签. 标签格式为 `(\#eq:label)`, 其中`eq`是关键字，例如
```
\begin{equation} 
  f\left(k\right) = \binom{n}{k} p^k\left(1-p\right)^{n-k}
  (\#eq:binom)
\end{equation} 
```


显示为
\begin{equation} 
  f\left(k\right) = \binom{n}{k} p^k\left(1-p\right)^{n-k}
  (\#eq:binom)
\end{equation} 
对于多行公式可以采用`align`环境，可对多个公式同时进行设置标签，不需要标签则用`\notag`，例如
```
\begin{align} 
g(X_{n}) &= g(\theta)+g'({\tilde{\theta}})(X_{n}-\theta) \notag \\
\sqrt{n}[g(X_{n})-g(\theta)] &= g'\left({\tilde{\theta}}\right)
  \sqrt{n}[X_{n}-\theta ] (\#eq:align)
\end{align}
```
显示为
\begin{align} 
g(X_{n}) &= g(\theta)+g'({\tilde{\theta}})(X_{n}-\theta) \notag \\
\sqrt{n}[g(X_{n})-g(\theta)] &= g'\left({\tilde{\theta}}\right)
  \sqrt{n}[X_{n}-\theta ] (\#eq:align)
\end{align}

## 定理标签的设定 {#sec4-2}

\indent
这里我们先叙述几个定义和定理，并给出几个例子.

\BeginKnitrBlock{lemma}<div class="lemma"><span class="lemma" id="lem:lem4-1"><strong>(\#lem:lem4-1) </strong></span>A group having an infinite number of elements.</div>\EndKnitrBlock{lemma}


\BeginKnitrBlock{theorem}\iffalse{-91-26080-38480-32676-93-}\fi{}<div class="theorem"><span class="theorem" id="thm:thm4-1"><strong>(\#thm:thm4-1)  \iffalse (无限群) \fi{} </strong></span>A group having an infinite number of elements.</div>\EndKnitrBlock{theorem}

\BeginKnitrBlock{proof}<div class="proof">\iffalse{} <span class="proof"><em>证明: </em></span>  \fi{}The proof comes here.</div>\EndKnitrBlock{proof}

\BeginKnitrBlock{definition}<div class="definition"><span class="definition" id="def:def4-1"><strong>(\#def:def4-1) </strong></span>A group having an infinite number of elements.</div>\EndKnitrBlock{definition}


\BeginKnitrBlock{example}<div class="example"><span class="example" id="exm:exm4-1"><strong>(\#exm:exm4-1) </strong></span>The set $(\mathbb{Z}, +)$ is an infinite group.</div>\EndKnitrBlock{example}


## 定理与公式的引用 {#sec4-3}

\indent
例\@ref(exm:exm4-1), 定义\@ref(def:def4-1) 定理\@ref(thm:thm4-1)为定理类引用.

公式的引用采用 `\@ref(eq:label)`, 例如上面的二个公式可引用为：
公式\@ref(eq:binom) 和公式 \@ref(eq:align). 

## 数学公式的扩展 {#sec4-4}

\indent
有些公式无法用$\TeX$中包的命令来实现，例如粗体数学符号，尽管在$\TeX$中有个`bm`包在数学环境下通过`\bm{\alpha}` 来实现`\boldsymbol{\alpha}`的功能，但在`html`下需要给`mathjax`做个$\TeX$宏(`macro`)^[配置在`MathJax.Hub.Config`下进行，具体参见Mathjax技术文档说明]:
```
  TeX: {
    extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"]
    Macros: {
      bm: ["{\\boldsymbol #1}",1],
    },
  }
```
此时由`$\bm{\alpha}$`出来的效果为 $\bm{\alpha}$. 

有关数据公式的标签与应用可参考[mathjax官方文档](https://www.mathjax.org/), `Mathjax`的本地化安装参考第\@ref(biber)章介绍.

\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]

