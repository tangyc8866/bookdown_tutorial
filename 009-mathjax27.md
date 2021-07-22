\cleardoublepage 

# (APPENDIX) 附录 {-}

# `Mathjax`的离线安装与使用 {#mjx}

\indent
附录\@ref(mjx)介绍了网页显示数学公式的插件mathjax，本地化安装，使用方法等. [@xie2015; @R-base]

## mathjax 说明  {#sec9-1}

- [MathJax](https://www.mathjax.org/)是一款相当强悍的在网页显示数学公式的插件。基于`Mathjax`, 通过$\LaTeX$的命令输出精美的数学公式. 加载Mathjax后^[需要运程或本地支持]，就可通过一对美元符号`$`(或左`\(`右 `\)`)输入行内公式，通过一对双美元符号`$$`(或左`\[`右`\]`)输入行间公式，例如

  ```
$$
J\alpha(x) = \sum{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}
$$
  ```
显示出下面的数学公式
$$
J\alpha(x) = \sum{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}
$$
- 可以使用$\LaTeX$自带的复杂的数学环境，如排版多行公式的`align`, `split`和数学字体命令，如`\mathscr`

```
\begin{align}
3x-1 &= \mathbb{A} \\
  3x &= \mathbf{B} \\
   x &= \mathscr{C}
\end{align}
```

输出为
\begin{align}
3x-1 &= \mathbb{A} \\
  3x &= \mathbf{B} \\
   x &= \mathscr{C}
\end{align}


## 调用远程服务器上的`mathjax`  {#sec9-2}

\indent
一般情况下，只需要使用远程加载`Mathjax`的`js`库就行了，例如在需要渲染数学公式的网页上增加`html`命令

```
</script>
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

## `mathjax`本地服务器的安装与使用 {#sec9-3} 


\indent
我们以`Macbook`的`Apache`服务器为例说明步骤^[Windows 10下的本地服务器的启动可参考(https://www.jianshu.com/p/d86c77942181)]

1. 服务器的启动

在终端(terminal)下输入命令
```
sudo apachectl start
```

2. 检查服务是否启动成功

在浏览器中输入网址
```
http://127.0.0.1/ 
```
如果显示`It Works!`就表示服务器已经成功启动。请记住:服务器上文件在本地的位置为

```
/Library/WebServer/Documents
```

3. 关闭服务器(不用时)

在终端(terminal)下输入命令
```
sudo apachectl stop
```

4. 将`Mathjax2.6`或`Mathjax2.7`下载并解压(安装)到`/Library/WebServer/Documents`下^[不要用最新的3.1版本], 目录名为`Mathjax`

5. 启动本地`Mathjax`

在运行`Bookdown`(或其他`rmarkdown`文件)时，须加载下面的`html`命令，在`Bookdown`中放在文件`mathjax_header.html`中，并由`_output.yml`加载进来. 

```
</script>
<script type="text/javascript"
   src="http://127.0.0.1/MathJax/MathJax.js">
</script>
```


\printbibliography[segment=\therefsegment, heading=subbibliography, title={参考文献}]
